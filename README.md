![github](https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=GitHub&logoColor=white)

My Gitbooks page (where I share HTB and Vulnhub box walkthroughs) - https://noelatvitb.gitbook.io/

My Gitbooks page (where I share Let's Defend Investigation Walkthroughs) - https://noelatvitb.gitbook.io/blue-team-investigations/

### Hi there,I am Noel Varghese 👋


:wink: I am an undergraduate student pursuing Btech in CSE specialization in Cyber Security, at Vellore Institute of Technology, Bhopal. I am an a Cybersecurity enthusiast - having  having experience working in Secure Coding,OSINT,Pentesting & Threat Intelligence fields

:bulb: Now, I am branching my journey towards Blue Teaming, where I will be documenting my journey and cases I solve from LetsDefend and Rangeforce platforms,on my blog hosted on Gitbooks

👨‍💻️ Retaining an interest in Secure Coding, I have participated in University level Secure Coding Tournaments, achieving 3'rd rank in OWASP Bangalore Chapter and 38'th rank in Devlymics Champions Tournament, conducted by Secure Code Warriors, Australia

## View my project 'Secode':A static code analyzer,that points insecure C language functions in your code and suggests secure alternatives - https://github.com/NoelV11/Secode

🕵 Contributed to Darkwebathon,hosted by the Anti-Human Trafficking Intelligence Initiative (@TeamATII).During this event,we the help of a 200+ search party scoured the Dark Web,pulled information from tools like Project Hades and Maltego,to identify individuals who operate in gambling,child porn and CSAM rings


👱 Cyber Security interests me as an individual, being the subject I am majoring in. Finding new techniques to enforce security in everyday life, and resisting attack attempts is thrilling and requires a whole lot of collective efforts from security professionals and general citizens, to make the world a much secure place. I would very much want to be a part of it

:sparkler: I am an advocate for incorporating women into the field of Cyber Security,owing to remove the gate barriers that they face.This led me to be a member of my University's Women in Cyber Security (WiCYS) Chapter.I try to contribute,to the best of my ability,for the good of this organization

:thought_balloon: Empowering them,by sharing nuggets of knowlege and providing them opportunities to forster their growth gives me immense joy

![](https://komarev.com/ghpvc/?username=NoelV11)

### 🔭 My Skills

- Worked with tools used in SOC Analyst environments - like WireShark,Yara, Virus Total and Sandboxes

- Threat Intelligence

- OSINT

- Blogging and Content Writing

### 🌱 Experience

- Interned at NTRDC,Crime Free Bharat,under the Threat Intelligence domain

- Interned at Haryana Police Crime Cell,under the Cyber Security domain
 
- Core Team Member,R&D (Research and Development) of VITB Cyber Warriors Club at VIT Bhopal

### 🤔 Get in touch

I am always open to meeting new people and opportunities

😄 Connect with me on Linkedin-https://www.linkedin.com/in/noel--varghese/

💬 Email- noelatvitb@gmail.com

📫 Fancy having a look at my Technical blog,? view them here-https://medium.com/@noelatvitb

👯 Thank you for viewing my GitHub Profile!

![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=NoelV11&count_private=true&theme=great-gatsby&show_icons=true)


## View my latest article!
<a target="_blank" href="https://github-readme-medium-recent-article.vercel.app/medium/@noelatvitb/0"><img src="https://github-readme-medium-recent-article.vercel.app/medium/@noelatvitb/0" alt="Recent Article 0"> 

 import requests
import base64
from bs4 import BeautifulSoup


profile_url = "https://tryhackme.com/badge/353765"      # Get this link from your Public Profile -> "Get Profile Badge ID" page
user_agent = {"User-agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.1 Safari/605.1.15"}

response = requests.get(profile_url, headers=user_agent)


if (response.status_code == 200):
    encoded = response.text.replace("document.write(window.atob(\"", "")
    encoded = encoded.replace("\"))", "")
else:
    print ("Request blocked by the TryHackMe CloudFlare interstitial.")
    exit()
    

decoded = base64.b64decode(encoded)
parsed = BeautifulSoup(decoded, 'html.parser')


user = parsed.findAll('span',{"class":"thm_nickname"})[0].text                  # <span class="thm_nickname">snkhan</span>          // Username
level = parsed.findAll('span',{"class":"thm_rank"})[0].text                     # <span class="thm_rank">[0x8][Hacker]</span>       // Level
rank = int(parsed.findAll('span',{"class":"thm_stat thm_mr"})[0].text)          # <span class="thm_stat thm_mr">9760</span>         // Global Rank
completedrooms = parsed.findAll('span',{"class":"thm_stat thm_mr"})[1].text     # <span class="thm_stat thm_mr">27</span>           // Rooms Completed
badges = parsed.findAll('span',{"class":"thm_stat"})[2].text                    # <span class="thm_stat">8</span>                   // Badges


thm = {}
for value in ["user", "level", "rank", "completedrooms", "badges"]:
    thm[value] = eval(value)


print (f'The user {thm["user"]} has a global rank of {thm["rank"]:,} with a title of {thm["level"]}. A total of {thm["completedrooms"]} rooms have been completed, with {thm["badges"]} badges awarded.')
