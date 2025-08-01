# 💾 Persistència de dades amb Docker a GitHub Codespaces

Aquest projecte mostra com provar **persistència real de dades entre contenidors Docker** dins de **GitHub Codespaces**, simulant un entorn com Azure Files.

---

## 🔍 Què es demostra?

- Crear un **volum Docker** persistent.
- Llançar un contenidor que escriu dades al volum. Eixir d'ell. Borrar-lo.
- Llançar un segon contenidor que llegeix aquestes dades. Que n'escriga d'altres i que cree una carpeta. Eixir d'ell. Borrar-lo.
- Llançarem un 3r contenidor i que comprove que hi està tot
- Tot dins d’un entorn **realment persistent** com és GitHub Codespaces.
- -Finalment borrare'm el volum persistent

---

## 🚀 Com executar

1. Obre aquest repositori a **GitHub Codespaces**.
2. Executa:

```bash
$ docker -it --name alpine1 -v persistent:/dades alpine
# echo 'Text de Demo 1' > /dades/demo1.txt
# exit
```

3. Després:

```bash
$ docker ps -a
$ docker stop alpine1
$ docker rm alpine1
$ docker -it --name alpine2 -v persistent:/dades alpine
# echo 'Text de Demo 2' > /dades/demo2.txt
# cd /dades
# mkdir carpeta
# ls
# exit
```

---

## 🧠 Què és `.devcontainer/`?

La carpeta `.devcontainer/` conté la configuració per a **Dev Containers**, que és com GitHub Codespaces (i VS Code) defineixen l'entorn de desenvolupament.

Això ens permet:
- Tenir **Docker instal·lat i funcional dins del Codespace**.
- Preinstal·lar extensions útils (com l’extensió de Docker per VS Code).
- Executar ordres inicials com `docker version` per verificar que Docker funciona.

---

## 📁 Contingut del projecte

| Arxiu / Carpeta             | Descripció                                                                 |
|-----------------------------|----------------------------------------------------------------------------|
| `.devcontainer/devcontainer.json` | Configura Docker dins de Codespaces.                                     |
| `docker-compose.yml`        | Defineix dos contenidors que comparteixen un volum persistent.            |
| `README.md`                 | Aquest document explicatiu.                                               |

---

## ✅ Persistència garantida

Els volums Docker creats dins de Codespaces **persistiran mentre el repositori i el codespace existeixin**. No es perden quan s’aturen contenidors.

---

## 🔚 Notes finals

Això és útil per:
- Fer proves de persistència de dades.
- Simular comportament de serveis com Azure Files.
- Entendre com compartir dades entre contenidors.
