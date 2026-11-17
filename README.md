# August Cyber GitHub Action (`augstai/august-action`)

Pull-request authorization and API boundary gate powered by [August Cyber](https://august.so). Diffs routes changed in a pull request, probes cross-account access across two test actors, emits inline GitHub annotations, and fails the check (`exit 2`) if cross-tenant exposure is reproduced.

## Usage

```yaml
name: August Cyber Gate
on:
  pull_request:
    branches: [main]

jobs:
  red-team-gate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: augstai/august-action@v1
        with:
          api-key: ${{ secrets.AUGUST_API_KEY }}
          base: origin/main
          address: 127.0.0.1:3000
          actor-a: "Authorization: Bearer ${{ secrets.STAGING_USER_A }}"
          actor-b: "Authorization: Bearer ${{ secrets.STAGING_OWNER_B }}"
```
