# XipFax

Fax any document to any fax number from Claude Code, or from Claude with this plugin. Add your pages from your computer or your phone, check the fax before it goes, and get its confirmation once it's delivered. Faxing the IRS? XipFax also finds the fax number of the IRS office that takes your form or notice.

## What it adds

- **XipFax's connector,** at `https://mcp.xipfax.com/mcp`. Three of its tools need no sign-in: a fax's price, a link to XipFax's send screen with the number filled in, and finding an IRS office's fax number. The rest act on your XipFax account once you sign in: putting your pages on your draft, sending it, and reading how a fax went and its confirmation.
- **The Send a fax skill,** `/xipfax:send-a-fax`, which takes Claude through those tools in order.

## What it sends, and where

- **To XipFax:** what you ask it to fax and the number it goes to, and for an IRS office's number, the form and the place you give.
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
