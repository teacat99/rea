# Fork synchronization

This fork backs up `morluto/rea`'s `main` every day at **03:17 Asia/Shanghai** (19:17 UTC). GitHub may delay scheduled runs. Run **Sync upstream main** manually from the Actions tab when needed.

The workflow uses GitHub's merge-upstream API. It preserves fork-only commits, including this documentation and the sync workflow, and stops on merge conflicts. It does not force-push, reset, delete branches, or run upstream application code. After synchronization it checks that the upstream commit observed at the start is included in the fork's history. The fork can therefore show commits ahead of upstream even while fully synchronized.

Only `main` is synchronized. Other branches, tags, release attachments, issues, and discussions are outside this backup's scope.

The built-in `GITHUB_TOKEN` has `contents: write` for merging and `actions: write` for disabling inherited workflows. Build and release workflows are disabled before and after each synchronization; only this sync workflow remains active. No personal token or deploy key is stored in the repository by this configuration.

To pause or resume, disable or enable **Sync upstream main** in the Actions tab. Run failures appear there; email notifications depend on the account's Actions notification settings. Public-repository schedules may be disabled after 60 days without repository activity. Check the workflow state or re-enable it if the upstream project has been idle for a long time.

If GitHub rejects a future merge because upstream workflow files require additional permissions, the run fails without discarding fork commits. Review the reported permission error before adding a repository-scoped credential.
