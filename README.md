# exit-status-guard

**This repository is archived and read-only. exit-status-guard now ships from
[karlkfi/claude-bouncer](https://github.com/karlkfi/claude-bouncer).**

```
/plugin marketplace add karlkfi/claude-bouncer
/plugin install exit-status-guard@claude-bouncer
```

Those two lines replace the pair this repo used to document. The plugin's
interface did not change — same three rules, same `.claude/exit-status-guard.json`,
same `EXIT_STATUS_GUARD_OVERRIDE=<reason>` prefix, same
`/exit-status-guard:friction-report`. Nothing in your own repo needs editing.

The five guards — `workspace-guard`, `branch-guard`, `prod-guard`,
`exit-status-guard`, `foreground-guard` — all parse the same Bash command
strings, and were re-implementing that parser five times over. They share one
now, so they share a repository, a test suite, and a release pipeline.

## Where the docs went

[`plugins/exit-status-guard`](https://github.com/karlkfi/claude-bouncer/tree/main/plugins/exit-status-guard)
in claude-bouncer: the three lost-status shapes, what the guard deliberately does
not deny, the config reference, the friction report, and the
[design notes](https://github.com/karlkfi/claude-bouncer/blob/main/plugins/exit-status-guard/docs/design.md).

Read that rather than anything in this repo. The last release here was `v2.0.0`
and the copy in claude-bouncer is ahead of it, so the pages under `docs/` here
describe behavior the shipping plugin no longer has.

## Switching an existing install

The marketplace name changes from `exit-status-guard` to `claude-bouncer`, so an
existing install has to be removed and re-added — an update will not cross that
boundary, and the old marketplace still clones fine, so nothing tells you it has
gone quiet:

```
claude plugin uninstall exit-status-guard@exit-status-guard
claude plugin marketplace remove exit-status-guard
claude plugin marketplace add karlkfi/claude-bouncer
claude plugin install exit-status-guard@claude-bouncer
```

Restart Claude Code (or `/reload-plugins`) to apply. The `/plugin` menu does the
same four steps interactively, on the CLI, the IDE extensions, and Claude Code
for Claude Desktop.

Still on 1.x? Its install record is `pipe-guard@pipe-guard` from a marketplace
named `pipe-guard`, so substitute those two names into the first two commands.
The 1.x configuration names go on working either way — `PIPE_GUARD_OVERRIDE=`
and `.claude/pipe-guard.json` are undocumented, not deprecated.

**Repoint auto-update too.** If you followed the old install instructions you
have an `extraKnownMarketplaces` entry in `~/.claude/settings.json` naming this
repository, and it will go on refreshing a marketplace that will never publish
another release. Replace it:

```json
{
  "extraKnownMarketplaces": {
    "claude-bouncer": {
      "source": { "source": "git", "url": "https://github.com/karlkfi/claude-bouncer.git" },
      "autoUpdate": true
    }
  }
}
```

The four sibling guards are one `install` line each against that same
marketplace — see the
[claude-bouncer README](https://github.com/karlkfi/claude-bouncer#install).

## What is still here

History, and the links that point into it. Archiving keeps every issue, pull
request and tag resolving; it does not delete them. New issues and pull requests
belong on
[claude-bouncer](https://github.com/karlkfi/claude-bouncer/issues). The
pre-move documentation is readable at the
[`v2.0.0`](https://github.com/karlkfi/claude-exit-status-guard/tree/v2.0.0) tag.

An installed 2.0.0 copy still names this repository's issue tracker in its deny
text, which an archived repo cannot accept. File those on claude-bouncer too —
or upgrade, since the shipping copy names the right one.

## License

[MIT](LICENSE)
