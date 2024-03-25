Once issue is fixed, run the tests and then patch-check:

```bash
## run tests
./python -m test -j8

## run patcheck script for linting and cleanup
make patchcheck
```

Commit your changes -> `gh-NNNN: <DESCRIPTION>` where `NNNN` is the issue number you helped solve.

First time contributors need to sign a CLA. -> [more info](https://devguide.python.org/getting-started/pull-request-lifecycle/#cla)

---

[reviewing a pr](https://devguide.python.org/getting-started/pull-request-lifecycle/#how-to-review-a-pull-request)

[where to get help](https://devguide.python.org/)

---

[currently reading](https://devguide.python.org/developer-workflow/communication-channels/)

