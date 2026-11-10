# XipFax

Fax a form from Claude Code, or from Claude with this plugin. XipFax finds the fax number of the IRS office that takes your form or notice, puts your pages on a fax, and lets you check it before it goes.

## What it adds

- **XipFax's connector,** at `https://mcp.xipfax.com/mcp`. Three of its tools need no sign-in: finding an office's fax number, a fax's price, and a link to XipFax's send screen with the number filled in. The rest act on your XipFax account once you sign in: putting your pages on your draft, sending it, and reading how a fax went and its confirmation.
- **The Fax a form skill,** `/xipfax:fax-a-form`, which takes Claude through those tools in order.

## What it sends, and where

- **To XipFax:** what you ask it to fax, the form's name, the place you give, and the number it goes to.
- **Your file, from your computer:** Claude uploads it to the one address XipFax gives for that file, good for 15 minutes.
- **A PDF at a link:** XipFax fetches it from the link you give.
- **Nothing else.** The plugin keeps nothing itself.

## Sign in

Run `/mcp`, choose `plugin:xipfax:xipfax`, and sign in to XipFax in your browser. Check the account shown, then choose Allow.

## Sending

Claude asks before it sends. Without a XipFax plan, you get a link where you look the fax over, send it and pay. On a plan, you choose whether faxes go straight away or come to you first.

## Privacy, terms and help

- [Privacy policy](https://xipfax.com/legal/privacy)
- [Terms](https://xipfax.com/legal/terms)
- [Contact us](https://xipfax.com/contact)
