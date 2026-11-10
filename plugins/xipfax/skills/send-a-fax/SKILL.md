---
name: send-a-fax
description: Fax any document to any fax number with XipFax's tools. Puts the person's pages on a fax, from their computer or their phone, gives the fax's price, and sends it from their XipFax account, or gives them a link to XipFax's send screen with the number filled in; then says how it went and gives its confirmation once it's delivered. Faxing the IRS, it also finds the fax number of the IRS office that takes their form or notice. Use when someone wants to fax a document, such as a signed lease to a landlord or a claim to an insurer.
---

# Send a fax

XipFax's MCP server has the tools. Use them in this order.

## 1. What to fax, and where

Ask the person what they want to fax, and the fax number it goes to.

If they're faxing an IRS office and don't have its number, call `find_fax_number` with what
they're sending, by its name or number, such as Form 2848, SS-4 or CP2000. If they've said where
they live, or where their business is, pass that as `place` too. For anyone else, ask the person
for the number: XipFax's list holds IRS offices alone.

`find_fax_number`'s `result` is one of three:

- `found`: the office is in `office`. Tell the person its name and fax number. If `instead` lists
  any offices, tell them those too, with whom each is for. If `signed_in_ink` is true, tell the
  person the office takes the form only signed by hand, in ink. If `confidential_cover` is true,
  the office asks for a cover sheet marked Confidential, which XipFax's send screen marks.
- `choose`: ask the person the `question`. Then call again with their answer, or take the office
  in `choices` that fits it.
- `none`: tell the person what `note` says. If they find a number on the form, on the notice or on
  the office's own page, `send_fax_link` and `send_fax` take it as `fax_number`.

## 2. Give the price

Once you know how many pages the fax has, call `quote_fax` with that number. Each document the
file tools put on a draft comes back with its pages. `quote_fax` gives the price of a fax without
a plan. A fax sent on a XipFax plan counts its pages on the plan instead. Tell the person the
number, the office where there is one, and the price, and send nothing until they say to send it.

## 3. Send it

The person chooses one of two ways.

**From XipFax's send screen.** Call `send_fax_link` with the `fax_number`, or with the `office_id`
that `find_fax_number` gave. It answers with a link to XipFax's send screen, the number already
filled in. Give the person the link: they add their pages there, sign in and pay. This way needs no
sign-in here.

**From here.** The other tools act on the person's XipFax account, so the first of them asks the
person to sign in. First put their pages on their draft:

- For a PDF on the computer you run commands on, call `add_fax_file`, make the upload its answer
  describes, then call `finish_fax_file`. A photo, or any other kind of file, goes as a PDF first;
  `add_fax_file` says how to make one.
- For a PDF at a public link, call `add_fax_file_from_url`.
- For a file you can't reach, such as one on their phone or one attached to this chat, call
  `add_fax_file_link`. Give the address only to the person. Once they say they're done adding their
  pages, call `finish_fax_file_link`.

Then call `send_fax` with the `fax_number` or the `office_id`, and every document's id in the order
you added them. Its `result` tells you what happened:

- `sent`: the fax is on its way. Keep `fax.id`, which `get_fax` reads.
- `waiting`: nothing has been sent. Give the person the `url`: they look the fax over there and
  send it, and pay there if they have no plan.
- `add_pages` or `look_over`: give the person the `url`, where they add their pages or check them.

Tell the person a fax went only when `result` is `sent`. If `send_fax` fails because XipFax didn't
say whether the fax went, don't send it again: ask the person to check their fax log in XipFax
first.

## 4. After it's sent

`get_fax`, given the fax's id, says how the fax is going: still sending, delivered, or failed and
why. Once it's delivered, `get_fax_confirmation` gives a link to its confirmation, a one-page PDF
the person can keep or pass on. The link works for a few minutes.
