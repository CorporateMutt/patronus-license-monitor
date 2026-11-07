# patronus-license-monitor

Uptime monitor for the Patronus license server
(`https://license.patronus-siem.com`, Fly app `patronus-license`).

The [`uptime`](.github/workflows/uptime.yml) workflow checks `/health` every
5 minutes with TLS verification and fails after 3 consecutive bad attempts.
GitHub emails the account that last edited the schedule when a run fails.

This repo is public on purpose: public repos get unlimited GitHub Actions
minutes, and a 5-minute check would otherwise exhaust a private repo's quota.
It contains no secrets; the health URL is already public.

**If you get an alert:**

```bash
fly status -a patronus-license
fly logs -a patronus-license
fly machine restart 48edde4b4537d8 -a patronus-license
```

Running Splunk installs keep working for 30 days without a successful
check-in. New license activations fail while the server is down.

Run a check on demand: Actions → *License server uptime* → *Run workflow*.
