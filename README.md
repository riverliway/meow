# Classify Financial Transactions

The HCB API provides the [following information](https://hcb.hackclub.com/docs/api/v3/schemas/Transaction) for each transaction:

`amount_cents` **integer** - the number of cents for this transaction

`memo` **string** - a sentence representing what the transaction is about

`date` **string** - the date for the transaction (format unknown)

`type` **invoice, donation, ach_transfer, check, transfer, bank_account_transaction, card_charge** - how the transaction was processed (convert to int-enum)

`organization.category` **hackathon, hack_club, nonprofit, event, high_school_hackathon, robotics_team, hardware_grant, hack_club_hq, outernet_guild, grant_recipient, salary, ai, hcb_internals** - what type of organization this is for (convert to int-enum)

`tags.label` **string** - the label for the current tags on this transaction (target for prediction)

In addition, there are several optional fields for each payment type. Each of them have a `memo` field.



## Architecture Ideas

First embed the memo and check to see if there is another embedded memo with a tag. If so, return that tag.

We can use weak supervision to run the untagged transactions through a generative LLM.

We can use strong supervision with the tagged transactions to train a custom model from scratch.
