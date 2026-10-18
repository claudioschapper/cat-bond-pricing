# Cat Bond Pricing

BXQF project development track, project 3. We price one parametric earthquake
catastrophe bond end to end and test whether its spread is fair for the risk.

Pipeline: USGS earthquake catalog -> fit rate (lambda) and b-value ->
Monte Carlo expected loss on the bond -> compare risk multiple
(spread / expected loss) with real deals from Artemis.bm.

## Roles and folders

| Role | Owner | Folder | Output |
|---|---|---|---|
| A. Hazard data | _name_ | `src/hazard/` | `data/catalog.parquet` |
| B. Fitting | _name_ | `src/fit/` | `params/hazard.json` |
| C. Bond and Monte Carlo engine | _name_ | `src/engine/` | `results/el.csv` |
| D. Market data and lead | _name_ | `src/market/` | `data/deals.csv` |

Reviewer pairs: A reviews B, B reviews C, C reviews D, D reviews A.

## Folder map

- `config/` bond definition (`bond.yaml`: region box, magnitude thresholds, payout steps, term, limit)
- `data/` cleaned data shared between roles (raw downloads go in `data/raw/`, which is git-ignored)
- `src/` code, one subfolder per role
- `params/` fitted hazard parameters
- `results/` model outputs
- `notebooks/` exploration only; numbers in the report must come from code in `src/`
- `report/` write-up and slides

## Setup

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Workflow

1. `git checkout main && git pull`
2. `git checkout -b <role letter>/<short-task-name>`, for example `a/decluster-catalog`
3. Commit small, push, open a pull request, request your reviewer
4. Merge after approval; delete the branch

Never commit directly to `main`. Use fixed random seeds in every Monte Carlo run.
