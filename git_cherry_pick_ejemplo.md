
# Ejemplo: git cherry-pick de feature → main

## Pre-requisitos
- Git instalado.
- Terminal abierta.
- (Opcional) Un repo vacío para practicar.

---

## Parte A — Cherry-pick limpio (un commit)

1) **Crear repo de práctica**
```bash
mkdir demo-cherry && cd demo-cherry
git init
echo "v1" > app.txt
git add app.txt
git commit -m "main: versión inicial"
```

2) **Crear rama `feature` y hacer 2 commits**
```bash
git switch -c feature
echo "linea A (feature)" >> app.txt
git commit -am "feature: agrega linea A"
echo "linea B (feature)" >> app.txt
git commit -am "feature: agrega linea B"
```

3) **Identificar el commit que quieres traer a `main`**
```bash
git log --oneline -2
```

4) **Cambiar a `main` y hacer el cherry-pick**
```bash
git switch main
git cherry-pick <HASH-de-agrega-linea-B>
```

5) **Verificar resultado**
```bash
git log --oneline --graph --decorate --all
cat app.txt
```

✅ Listo: trajiste **solo** ese commit de `feature` a `main` sin mezclar todo lo demás.

---

## Parte B — Cherry-pick de varios commits

### 1. Commits contiguos (rango):
```bash
git switch feature
git log --oneline
git switch main
git cherry-pick <HASH-C1>^..<HASH-C3>
```

### 2. Commits sueltos (no contiguos):
```bash
git switch main
git cherry-pick <HASH-X> <HASH-Y> <HASH-Z>
```

---

## Parte C — Ejercicio con conflicto y cómo resolverlo

1) **Reinicia el estado rápido (opcional)**
```bash
rm -rf .git && git init
echo "color=blue" > config.txt
git add config.txt
git commit -m "main: base color=blue"
```

2) **En `feature` cambiamos esa línea**
```bash
git switch -c feature
printf "color=green
" > config.txt
git commit -am "feature: cambia color a green"
```

3) **En `main` cambiamos la misma línea**
```bash
git switch main
printf "color=red
" > config.txt
git commit -am "main: cambia color a red"
```

4) **Intentar cherry-pick del commit de `feature`**
```bash
git cherry-pick <HASH-feature-green>
```
> Aparecerá: **CONFLICT (content): Merge conflict in config.txt**

5) **Resolver conflicto**
- Editar `config.txt` y dejar la versión final.
- Luego:
```bash
git add config.txt
git cherry-pick --continue
```

6) **Cancelar cherry-pick en curso**
```bash
git cherry-pick --abort
```

---

## Tips útiles

- Ver commits cortos:
```bash
git log --oneline --graph --decorate --all
```

- Adjuntar referencia al commit original:
```bash
git cherry-pick -x <HASH>
```

- Traer cambios sin crear commit:
```bash
git cherry-pick --no-commit <HASH>
# o
git cherry-pick -n <HASH>
git commit -m "main: trae cambios de feature agrupados"
```

- Cancelar en cualquier momento:
```bash
git cherry-pick --abort
```

---

## ¿Cuándo usar cherry-pick vs merge?

- **Cherry-pick**: para uno o pocos commits específicos.
- **Merge**: para integrar toda la rama.
- **Rebase**: para re-aplicar commits encima de otra base y mantener historia lineal.

---
