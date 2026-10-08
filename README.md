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

Le site est publié par le dépôt [cartiflette](https://github.com/InseeFrLab/cartiflette)
(`.github/workflows/docs.yml`), à l'adresse <https://inseefrlab.github.io/cartiflette/>,
avec la documentation technique sous `doc/` et le client de ce dépôt-là.

`.github/workflows/publish.yaml` :

- sur une pull request, rend le site (profil `complete`) pour le vérifier ;
- à chaque push sur `main`, demande au dépôt cartiflette de republier le site, et
  ne publie sur les GitHub Pages de ce dépôt qu'une redirection
  (`redirect/index.html`, servie aussi comme `404.html`) : les anciennes adresses
  `https://inseefrlab.github.io/cartiflette-website/...` renvoient vers la même page
  du nouveau site.
