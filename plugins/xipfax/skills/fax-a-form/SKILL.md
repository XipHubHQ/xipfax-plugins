---
name: fax-a-form
description: Fax a form, or a reply to a notice, to the IRS office that takes it, with XipFax's tools. Finds the office's fax number, gives the fax's price, and sends the person's pages from their XipFax account, or gives them a link to XipFax's send screen with the number filled in. Use when someone needs to fax a form such as Form 2848 or SS-4, or answer a notice such as a CP2000.
---

# Fax a form

XipFax's MCP server has the tools. Use them in this order.

## 1. Find where it goes

Ask for the form or notice by its name or number, such as Form 2848, SS-4 or CP2000. Then call
`find_fax_number` with it. If the person has said where they live, or where their business is,
pass that as `place` too.

Its `result` is one of three:

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
a plan. A fax sent on a XipFax plan counts its pages on the plan instead. Tell the person the office,
the number and the price, and send nothing until they say to send it.

## 3. Send it

The person chooses one of two ways.

**From XipFax's send screen.** Call `send_fax_link` with the `office_id` that `find_fax_number`
gave, or with a `fax_number`. It answers with a link to XipFax's send screen, the number already
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

Then call `send_fax` with the `office_id` or the `fax_number`, and every document's id in the order
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
