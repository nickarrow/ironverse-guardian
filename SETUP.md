# Guardian Repository Setup Guide

Follow these steps to set up the external Guardian monitoring system.

## Step 1: Initialize the Guardian Repository

```bash
# Clone the empty guardian repository
git clone https://github.com/nickarrow/the-foundry-guardian.git
cd the-foundry-guardian

# Copy files from the-foundry/guardian-repo-files/
# (You'll need to manually copy these files)

# Create directory structure
mkdir -p .github/workflows
mkdir -p canonical-workflows

# Copy the files:
# - Copy monitor.yml to .github/workflows/monitor.yml
# - Copy enforce-ownership.yml to canonical-workflows/enforce-ownership.yml
# - Copy enforce_ownership.py to canonical-workflows/enforce_ownership.py
# - Copy README.md to root
```

## Step 2: Create Personal Access Token

1. Go to: https://github.com/settings/tokens?type=beta
2. Click "Generate new token"
3. Configure:
   - **Token name**: `foundry-guardian-token`
   - **Expiration**: 1 year
   - **Repository access**: Only select repositories
     - Select: `nickarrow/the-foundry`
   - **Repository permissions**:
     - Contents: **Read and write**
     - Issues: **Read and write**
     - Metadata: Read-only (auto-selected)
4. Click "Generate token"
5. **COPY THE TOKEN** (you won't see it again!)

## Step 3: Add Token to Guardian Repository

1. Go to: https://github.com/nickarrow/the-foundry-guardian/settings/secrets/actions
2. Click "New repository secret"
3. Name: `FOUNDRY_PAT`
4. Value: Paste the token you copied
5. Click "Add secret"

## Step 4: Push Files to Guardian Repository

```bash
# In the-foundry-guardian directory
git add .
git commit -m "Initial Guardian setup"
git push origin main
```

## Step 5: Test the Guardian

1. Go to: https://github.com/nickarrow/the-foundry-guardian/actions
2. Click "Guardian - Monitor The Foundry" in the left sidebar
3. Click "Run workflow" button
4. Select branch: `main`
5. Click "Run workflow"

Wait for it to complete and check the logs. You should see:
```
✅ All workflow files are intact
```

## Step 6: Verify Scheduled Runs

The Guardian will now run automatically every 15 minutes. Check back in 15-30 minutes and you should see automatic runs appearing in the Actions tab.

## Testing Attack Detection (Optional)

To test that Guardian actually works:

1. In `the-foundry`, delete the enforcement workflow:
   ```bash
   cd the-foundry
   git rm .github/workflows/enforce-ownership.yml
   git commit -m "Test: Delete workflow"
   git push
   ```

2. Wait up to 15 minutes for Guardian to run

3. Check:
   - Guardian Actions logs should show "❌ MISSING" detection
   - `the-foundry` should have the workflow restored
   - A GitHub Issue should be created in `the-foundry`

4. Close the test issue and you're done!

## Troubleshooting

**Guardian not running?**
- Check that the workflow file is at `.github/workflows/monitor.yml`
- Verify scheduled workflows are enabled in repo settings
- Check Actions tab for any error messages

**Permission errors?**
- Verify the PAT is added as `FOUNDRY_PAT` secret
- Check that the PAT has Contents and Issues write permissions
- Ensure the PAT hasn't expired

**Can't find canonical files?**
- Verify files are in `canonical-workflows/` directory
- Check filenames match exactly: `enforce-ownership.yml` and `enforce_ownership.py`

## Success!

Once you see Guardian running every 15 minutes in the Actions tab, your external monitoring system is fully operational!

The Foundry is now protected by an external Guardian that cannot be disabled by attackers.
