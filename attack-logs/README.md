# Guardian Attack Logs

This directory contains automated logs of detected attacks on The Foundry repository.

## What Gets Logged

When Guardian detects compromised workflows in `the-foundry`, it automatically creates a detailed log file here with:

- **Timestamp** - When the attack was detected
- **Commit Information** - Last known good commit vs compromised commit
- **Attackers** - GitHub usernames and emails of commit authors involved
- **Malicious Commits** - List of all commits made during the attack
- **Files Affected** - What was deleted, modified, added, or renamed
- **Actions Taken** - How Guardian restored the repository
- **Recommended Actions** - Steps for admin to take

## Log File Format

```
attack_YYYY-MM-DD_HH-MM-SS.log
```

Example: `attack_2025-12-16_15-30-00.log`

## What To Do When You See a New Log

1. **Review the log file** - Check who the attackers are
2. **Verify it's not a mistake** - Sometimes legitimate users might accidentally trigger this
3. **Remove access** - Go to `the-foundry` Settings → Collaborators and remove write access for malicious users
4. **Monitor** - Watch for repeat attacks from the same users
5. **Investigate** - Check if accounts were compromised

## Security

- These logs are stored in the private `the-foundry-guardian` repository
- Only you have access to this repository
- Attackers cannot delete these logs (they don't have access to this repo)
- Logs are kept indefinitely for audit trail

## Retention

These logs are kept indefinitely. You can manually delete old logs if needed, but they're small text files and don't take up much space.
