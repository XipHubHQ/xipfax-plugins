# XipFax plugins

XipFax's plugin for Claude Code and for Codex. It connects your assistant to XipFax's MCP server,
at `https://mcp.xipfax.com/mcp`, and adds the Fax a form skill.

With the plugin, your assistant can:

- find the fax number of the IRS office that takes a form or a notice;
- give the price of a fax;
- give you a link to XipFax's send screen with the number filled in, where you add your pages,
  sign in and pay.

Once you sign in to XipFax, it can also:

- put your pages on a draft: a file on your computer, a PDF at a public link, or pages you add
  yourself on a page it gives you a link to;
- send the draft. It goes at once if you have a plan and chose Send straight away when you
  connected your assistant, or since. Otherwise you get a link where you look the fax over and
  send it, and pay there if you have no plan;
- say how a fax went, and give a delivered fax's confirmation.

## Claude Code

In Claude Code:

```
/plugin marketplace add XipHubHQ/xipfax-plugins
/plugin install xipfax@xipfax-plugins
```

Or from a shell:

```
claude plugin marketplace add XipHubHQ/xipfax-plugins
claude plugin install xipfax@xipfax-plugins
```

To sign in to XipFax, run `/mcp`, choose `plugin:xipfax:xipfax`, and sign in in your browser.
Then ask your assistant to fax a form, or run `/xipfax:fax-a-form`.

## Codex

```
codex plugin marketplace add XipHubHQ/xipfax-plugins
codex plugin add xipfax@xipfax-plugins
```

Then start a new session, and connect XipFax when Codex asks. Ask Codex to fax a form, or pick
`fax-a-form` in `/skills`.

## Privacy and terms

- [XipFax's privacy policy](https://xipfax.com/legal/privacy)
- [XipFax's terms](https://xipfax.com/legal/terms)

## Help

Write to XipFax from its [Contact page](https://xipfax.com/contact).
