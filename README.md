# cartiflette-website

Site de [cartiflette](https://github.com/InseeFrLab/cartiflette) : exemples et cas
d'usage, publié sur <https://inseefrlab.github.io/cartiflette/>.

## Construire le site

Les dépendances Python du rendu (client `cartiflette`, geopandas, matplotlib…) sont
gérées avec [uv](https://docs.astral.sh/uv/) (`pyproject.toml`, `uv.lock`) :

```bash
uv sync                                   # crée .venv à partir de uv.lock
export QUARTO_PYTHON="$PWD/.venv/bin/python"
quarto preview                            # accueil et « À propos »
QUARTO_PROFILE=complete quarto render     # avec les cas d'usage (use-case/)
```

Ajouter une dépendance : `uv add <paquet>`. Mettre à jour le client :
`uv lock --upgrade-package cartiflette`.

Pour essayer un client en développement (dépôt cartiflette cloné à côté) :

```bash
uv sync --no-install-package cartiflette
uv pip install ../cartiflette/python-package/cartiflette
```

## Publication

`.github/workflows/publish.yaml` rend le site (profil `complete`) à chaque push sur
`main` et le publie sur GitHub Pages. Il demande ensuite au dépôt cartiflette de
republier le site complet, qui y ajoute la documentation technique sous `doc/` et
utilise le client de ce dépôt-là (`docs.yml`).
