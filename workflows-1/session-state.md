# Session State

Use the session\_state to cache intermediate results in a database.

All Workflows come with a `session_state` dictionary that you can use to cache intermediate results. Provide your workflows with `storage` and a `session_id` to enable caching.

For example, you can use the `SqlWorkflowStorage` to cache results in a Sqlite database.

Copy

```
# Create the workflow
generate_blog_post = BlogPostGenerator(
    session_id="my-session-id",
    storage=SqlWorkflowStorage(
        table_name="generate_blog_post_workflows",
        db_file="tmp/workflows.db",
    ),
)
```

Then in the `run()` method, you can read from and add to the `session_state` as needed.

Copy

```

class BlogPostGenerator(Workflow):
    # ... agents
    def run(self, topic: str, use_cache: bool = True) -> Iterator[RunResponse]:
        # Read from the session state cache
        if use_cache and "blog_posts" in self.session_state:
            logger.info("Checking if cached blog post exists")
            for cached_blog_post in self.session_state["blog_posts"]:
                if cached_blog_post["topic"] == topic:
                    logger.info("Found cached blog post")
                    yield RunResponse(
                        run_id=self.run_id,
                        event=RunEvent.workflow_completed,
                        content=cached_blog_post["blog_post"],
                    )
                    return

        # ... generate the blog post

        # Save to session state for future runs
        if "blog_posts" not in self.session_state:
            self.session_state["blog_posts"] = []
        self.session_state["blog_posts"].append({"topic": topic, "blog_post": self.writer.run_response.content})
```

When the workflow starts, the `session_state` for that particular `session_id` is read from the database and when the workflow ends, the `session_state` is stored in the database.

You can always call `self.write_to_storage()` to save the `session_state` to the database at any time. Incase you need to abort the workflow but want to store the intermediate results.

View the [Blog Post Generator](https://docs.phidata.com/workflows/introduction#full-example-blog-post-generator) for an example of how to use session state for caching.
