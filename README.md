# Fuldskærms MP4-afspiller (Frontend + Admin via GitHub Pages)

En ren HTML-løsning bestående af en **fuldskærms-afspiller (`index.html`)** og et **admin-panel (`admin.html`)**, som gemmer playlisten direkte i `playlist.json` i dit offentlige GitHub-repository. Dermed kan du tilføje og sortere videoer fra mobil eller anden PC, mens storskærmen automatisk henter opdateringerne.

## Filer i projektet

- `index.html` – **Frontend / afspiller**: Viser første stillbillede af næste video, afspiller i fuld skærm ved tryk på **Mellemrum**, ignorerer Mellemrum under afspilning, skifter øjeblikkeligt til stillbilledet af næste video når den slutter, og starter forfra efter sidste video.
- `admin.html` – **Backend / admin-panel**: Tilføj MP4-links (eller vælg `.mp4`-filer direkte fra dit GitHub-repo), giv dem titler, slet og ændr rækkefølge med pile eller træk-og-slip, og gem direkte til GitHub.
- `playlist.json` – Den samlede playliste, som synkroniseres mellem admin og afspiller.
- `videos/` – Mappe til dine MP4-filer (maks. 100 MB pr. fil på GitHub).

---

## Opsætning på GitHub (5 minutter)

### 1. Opret et offentligt GitHub-repository
1. Opret et nyt **Public** repository på GitHub (f.eks. `Happynator`).
2. Upload filerne `index.html`, `admin.html`, `playlist.json` og mappen `videos/` til `main`-branchen.
3. Upload dine MP4-filer (under 100 MB pr. stk.) i mappen `videos/`.

### 2. Aktivér GitHub Pages
1. Gå til **Settings → Pages** i dit GitHub-repository.
2. Under **Build and deployment → Source**, vælg **Deploy from a branch**.
3. Vælg branch **main** og mappen **/ (root)**, og klik på **Save**.
4. Efter ca. 1 minut er dine to sider live:
   - **Frontend (storskærm):** `https://<dit-brugernavn>.github.io/<repo-navn>/`
   - **Backend (admin på mobil/PC):** `https://<dit-brugernavn>.github.io/<repo-navn>/admin.html`

### 3. Opret en sikker GitHub-nøgle (til `admin.html`)
For at du kan gemme ændringer i `playlist.json` fra din telefon eller anden computer uden en ekstern server, opretter du en begrænset GitHub-nøgle:

1. Gå til GitHub **Settings → Developer settings → Personal access tokens → Fine-grained tokens**.
2. Klik på **Generate new token** og giv den et navn (f.eks. `Happynator Admin`).
3. Under **Repository access**: vælg **Only select repositories** og vælg kun dette repository.
4. Under **Permissions → Repository permissions**: sæt **Contents** til **Read and write**.
5. Klik på **Generate token** og kopiér nøglen (`github_pat_...`).
6. Åbn `admin.html`, indsæt nøglen under **GitHub-forbindelse** og klik på **Forbind & hent playliste fra GitHub**.

> **Sikkerhed:** Nøglen gemmes kun lokalt i browseren på din admin-enhed (`localStorage`) og bliver aldrig lagt i dit repository. Afspilleren (`index.html`) kræver ingen nøgle eller login.

---

## Betjening i afspilleren (`index.html`)

| Tast / handling | Funktion |
| --- | --- |
| **Mellemrum (Space)** | Starter den viste video i fuld skærm (ignoreres mens videoen afspiller) |
| **F** (eller dobbeltklik) | Slår fuld skærm til/fra (god til at gøre klar på stillbillede #1 inden start) |
| **R** | Henter seneste `playlist.json` med det samme (opdaterer også automatisk hvert 90. sekund) |

## Tip vedrørende links til MP4-filer
- Når dine videoer ligger i samme GitHub-repository, er det bedste format en relativ sti som `videos/min-video.mp4` (eller brug knappen **"Find MP4-filer i GitHub-repo"** i `admin.html`). Det sikrer hurtig streaming via GitHub Pages.
- Hvis du kopierer et normalt GitHub-link (`https://github.com/.../blob/main/...`), omdanner `admin.html` og `index.html` det automatisk til et afspilbart videolink.
