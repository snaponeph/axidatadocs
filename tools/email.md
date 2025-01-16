---
description: >-
  EmailTools enable an Agent to send an email to a user. The Agent can send an
  email to a user with a specific subject and body.
---

# Email

#### Example <a href="#example" id="example"></a>

cookbook/tools/email\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.email import EmailTools

receiver_email = "<receiver_email>"
sender_email = "<sender_email>"
sender_name = "<sender_name>"
sender_passkey = "<sender_passkey>"

agent = Agent(
    tools=[
        EmailTools(
            receiver_email=receiver_email,
            sender_email=sender_email,
            sender_name=sender_name,
            sender_passkey=sender_passkey,
        )
    ]
)
agent.print_response("send an email to <receiver_email>")
```

#### [​](https://docs.phidata.com/tools/email#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`receiver_email`

`str`

\-

The email address of the receiver.

`sender_name`

`str`

\-

The name of the sender.

`sender_email`

`str`

\-

The email address of the sender.

`sender_passkey`

`str`

\-

The passkey for the sender’s email.

#### [​](https://docs.phidata.com/tools/email#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`email_user`

Emails the user with the given subject and body. Currently works with Gmail.

#### [​](https://docs.phidata.com/tools/email#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/email.py)
