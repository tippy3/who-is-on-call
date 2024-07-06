# Find On-Call from PagerDuty

A GitHub Action to get current on-call users from PagerDuty escalation policy.

## Usage

```yaml
jobs:
  find-oncall:
    runs-on: ubuntu-latest
    steps:
      - id: oncall
        uses: tippy3/who-is-on-call@main
        with:
          token: ${{ secrets.PAGERDUTY_TOKEN }}
          escalation_policy_name: ${{ secrets.PAGERDUTY_EP_NAME }}
      - run: |
          echo "${{ steps.oncall.outputs.all_users }}"
          echo "${{ steps.oncall.outputs.user }}"
```

## Inputs

```yaml
uses: tippy3/who-is-on-call@main
with:
  # [Required] PagerDuty API token or API key
  token: ''

  # Escalation policy ID
  escalation_policy_ID: ''

  # Escalation policy name. Either the ID or the name is required.
  escalation_policy_name: ''

  # Filter to get on-calls
  # Set 'Level=1' to get 1st responders or '' to get all responders.
  # Default: Level=1
  filter: ''
```

## Outputs

```bash
# All on-call users
echo '${{ steps.oncall.outputs.all_users }}'
ai.hoshino
akane.kurokawa
goro.amamiya
kana.arima

# Only the first user
echo '${{ steps.oncall.outputs.user }}'
ai.hoshino

# One user at random
echo '${{ steps.oncall.outputs.random_user }}'
kana.arima
```
