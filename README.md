# Vecka 34 – CI/CD Fördjupning

## 🔨 Praktiska övningar

### 🟢 Lätt

**Skapa ett grundläggande Pull Request-flöde**

1.  git checkout dev
    git pull origin dev
    git checkout -b feature/update-readme
    
2.  Gör en liten ändring i `README.md` (t.ex. lägg till en rad längst ner).
    
3.  git push -u origin feature/update-readme
    
4.  Öppna en Pull Request från feature/update-readme → dev i GitHub.
    

### 🟠 Medel

**Lägg till ett CI-test för Pull Requests**

1.  Skapa en fil .github/workflows/pr-check.yml.
    
2.  klistra in följande kod:
    ```yaml
    name: PR Check

    on:
      pull_request:
        branches: [ "dev" ]

    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v3
          - name: Use Node.js
            uses: actions/setup-node@v3
            with:
              node-version: '18'
          - run: npm install
          - run: npm test
    ```
    
3.  Committa och pusha workflow-filen till din branch och öppna en Pull Request.
    
4.  Se hur GitHub kör din pipeline innan du kan merge:a.
    

### 🔴 Svår

**Gör så att en PR måste passera tester innan merge**

1.  Gå till repo-inställningarna i GitHub, **Branches → Branch Protection Rules**.
    
2.  Lägg till en regel för dev som:
    
    *   Kräver Pull Request-granskning innan merge.
        
    *   Kräver att status checks (ditt PR Check-workflow) passerar.
        
3.  Testa att merge:a en PR där testerna failar — den ska blockeras.
    
4.  Fixa felet så att testerna går igenom och merge:a sedan.
    

💡 Tips
-------

*   Uppdatera alltid dev med senaste från main innan du startar en ny feature-branch.
    
*   Håll Pull Requests små och fokuserade så blir de enklare att granska.
    
*   Skriv tydliga commit-meddelanden även i feature-branches.
