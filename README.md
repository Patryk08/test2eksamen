Dokumentasjon på Eksammenn.py nettsiden 

I dag har jeg jobbet med min nettside. Jeg har endret litt på css, og byttet på farger på nettsiden. Jeg byttet farge på backround fra hvit til svar rød farge. 
Jeg har endret på tekst på nettsiden for å oppdatere status på ulike prosjekter. 

Veiledning på nettsiden

Dette er en enkelt flask app med bruk av css, html, python og flask. På home siden har du litt info om oss, Vår service og linker til våre prosjekter.
Med en gang du kommer på nettsiden så ser du velkommen til Nordtech solutions. Der har du en link til våre prosjekter i den blåe boksen til høyre. 
Der er det en blå link som følger deg til aktive prosjekter. Du kan og veilede deg på nettsiden ved bruk at de 2 knappene øverst til høyre side. 
Der har du en home knapp og en project knapp. 
Der har du prosjekter som nettsider og status på de. 

Dokumentasjon på prosessen og hoste denne appen på proxmox. 

jeg ssh inn å vm remotly, det gjor jeg for å sleppe å skrive inn alt manuelt og det er mer ryddig for meg. 
Jeg startet med å laste ned docker. da skrev jeg inn curl -fsSL https://get.docker.com | sh. det lastet ned docker
Da lastet jeg ned koden fra github. Da skrev jeg inn git pull og linken til githuben der hele koden ligger. 
Etter det var ferdig så skrev jeg inn ls for å se hva mapper ligger der. da kom det opp "test2eksamen" og det er der alle filene ligger. 
Via terminalen så konfigurerte eg docker compose, det er bare en blueprint for selve nettsiden. 

Her er innholdet i compose.yml som jeg brukte: 

name: eksamensapp
services:
  eksamensapp:
    build: .
    container_name: eksamensapp
    ports:
      - "80:5808"
    volumes:
      - /var/log/ny-app:/var/log/ny-app
    restart: always


Her kan du se navnet som er da eksamensapp. 
Den builder container som hetter eksamensapp, Port er satt til 5808. 
Og den restart er på always. 

Etter det var ferdig laget jeg en dockerfile via terminal inne i mappen, da skrev jeg inn nano Dockerfile, viktig med stor D.
Her er innholdet i dockerfilen:


FROM python:3.13-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 5808
CMD ["python", "Eksammenn.py"]

Det denne dockerfilen gjør er at Den velger base image som er da python:3.13-slim.
Den oppretter mappen som er da: WORKDIR /app
Den kopierer da requirements.txt som er da flask fordi den har flask som en requirement.
COPY .. kopierer den hele prosjektet
Expose 5858 gjør at porten er satt til 5808. 
Og CMD CMD ["python", "Eksammenn.py"] er det som kjører appen. 

Etter det Byttet jeg docker containeren som er: sudo docker compose up -d --build og den bygegr da appen. 
Nå på nettet skriver du inn Http://10.0.0.36 og da er du inpå nettsiden. 

Etter jeg var ferdig med det så oppdaterte jeg flask appen, jeg bytett på bakgrunn farge på nettsiden.
Jeg Pushet changes på github, så i terminalen skrev jeg inn git pull og det puller de nyeste endringene på github. 
Så skreiv jeg inn docker compose down får å slette den gamle containeren der den gamle nettsiden runnet. og bygget ny med å skrive sudo docker compose up -d --build. 
## Da er den nettsiden oppdatert. 
