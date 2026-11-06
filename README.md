# Lab: DAST in a GitHub Actions Pipeline

This lab runs an OWASP ZAP scan against DVWA on every push.
A quality gate fails the workflow when High-risk alerts are found.

## Files

```
.github/workflows/dast.yml   workflow definition (trigger, services, steps)
ci/setup_dvwa.py             waits for DVWA and creates its database
ci/zap_scan.py               logs in, runs spider + active scan, applies the gate
```

## Steps

1. Create a **public** repository on GitHub (Actions minutes are free for public repositories).
2. Push these files to the `main` branch.
3. Open the **Actions** tab and select the running **DAST scan** workflow.
4. When the run finishes (about 15–20 minutes):
   - Read the summary table on the run page.
   - Download the `zap-reports` artifact and open `zap-report.html`.
5. The run fails because DVWA at security level `low` has High alerts.

## Exercises

1. Change `SECURITY_LEVEL` in `dast.yml` to `impossible`, push, and compare the High alerts.
2. Pick one High alert and decide whether it is a true or false positive.
3. Change `MAX_HIGH` and explain why relaxing a quality gate is risky.

## Notes

- The scan target runs inside the workflow as a service container. Never scan systems you do not own.
- The ZAP API key is generated for each run and masked in the logs.