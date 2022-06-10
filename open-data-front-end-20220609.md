

---
# Open WIN  - Open Data Front End
## Agenda and collaborative notes 

-----

**Important information**

- Date/time: Thursday 9th June, 11:00-12:00
- Join the call: MS Teams
- These notes: [https://hackmd.io/@FE_yEojCQPW4PD8RcTWR0A/ryenANJY5](https://hackmd.io/@FE_yEojCQPW4PD8RcTWR0A/ryenANJY5)


<mark>Yellow = action</mark>


-----

## Agenda
1. Review decision matrix
2. Progress / challenges with c-kan and globes implementation. Pros and cons.
3. Review infrastructure decisions we’re confident with (e.g.  ORCID authentication)
4. Identify outstanding questions which need decision making input (e.g. acceptable requirement for external users to download a program to receive data via globus)
5. Present globus pricing structure and identify other interested (University) groups who are pursuing, supporting a drive for institutional subscription.


## Participants
(name / Pronouns / Department / git handles (GitLab) / ORCID ID)
1. Cassandra Gould van Praag / she/her / Psychiatry / @cassag; / 0000-0002-8584-4637
2. Mattew South / 
3. Duncan Smith / 
4. Duncan Mortimer / 
5. Dave Flitney / 
6. Stuart Clare / he/him / NDCN / what is a git handle? / 0000-0001-6421-9990
7. Tom Nichols / 

 
## Participation guidelines
- We value the participation of every member of our community and want to ensure that each of us has an enjoyable and fulfilling experience. Please show respect and courtesy to other community members at all times.
- We are dedicated to a harassment-free experience for everyone, regardless of gender, gender identity and expression, sexual orientation, disability, neurodiversity, physical appearance, body size, race, age, religion, politics or technology choices. We do not tolerate harassment by and/or of members of our community in any form.
- We welcome, support and respect eachother as whole people.
- We fall under the formal policy and reporting guidelines of the University of Oxford Bullying and Harassment Policy and we expect everyone to be a responsible bystander.

-----

## 1. Review decision matrix
- [Decision matrix mural](https://app.mural.co/invitation/mural/openwin9903/1648828688593?sender=uacde5bb1e1e121d1e4a43562&key=6254f6a0-cf8d-4e4c-95ea-4d5c7fb7e103) (works best on chrome)
- [Scoring the options](https://docs.google.com/spreadsheets/d/1_zE4RYf43uxrdEmqWJm_EaxCQ3Nrne4lGvA_ghBqhQk/edit?usp=sharing) (google sheet).

What are C-KAN and Globus
- C-KAN is an open source project for a data portal. 
    - Written in python. 
    - web database for sharing files of various types 
    - You clone and run yourself
    - Takes "files" - not restructions on data types
- Globus
    - Technology focus on sharing large files
    - configurable portals for the font end
    - Network of nodes across the world
    - file transfer system used by CERN and others
    - Your data can be discovered from globus.org (although clumsy). 
    - You create your node whic conencts to the network


Both support a range of authentication
- Globus: SSO, ORCID
- C-KAN: plugin architecture means it's probably been done in the past! 

### Test C-KAN instance
- [https://test-ckan.win.ox.ac.uk](https://test-ckan.win.ox.ac.uk) (requires university network)
- Data are bundelled into "organisations" and "groups" - this is one way we will be able to manage PI/group access.
- Using a default theme
- installed at Begbrooke with our XNAT resources (until we move to BMRC)
- Populated with default test data which come with the test package
- datasets can be associated with organisations and/or groups
- Viewing a dataset gives a list of files, which groups they're attached to and an activity log
- files can be previewed with where the appropraitge plug-in has been installed
- files can be downloaded individually or on mass
- out of the box previews were created by sending data back and forward to create a java view. We've now modified this to all happen at our end.
- Data upload shows configuable metadata fields.
- SC: Would we write something which pipes from our XNAT, or would users do it themselves?
    - MS: We should create something nice/easy to pipe
    - DS: There is also an extensive API
- TN: External authentication?
    - MS: You can set external visibility.
- TN: Applying different data usage agreements?
    - MS: We don't have an immeditate story for that, but it's within the remit of the tool. We just need the strategy for satisfy the case.
- DF: TPSA?
    - MS: The open foundation might provide some
    - TN: Novartis TPSA - had to require an external consultant to complete.
    - TN: What is the worst case scenario? Info Sec shut us down?
    - DM: As this is self-hosted, it should be in a different domain. 


### Globus
- Demo of file transfer (using the BMRC node)
- This is just a file manager. We'd still need to boly on a front end (c-kan like) to organise the data
- Colelctions of data would be gifted to you. If you requested access to something you would get a view of those files
- For users to send/receive, they need to download a tool (user client) - this is where it is made powerful in paralleleising data transfer.
- In the paid for version you can turn on file encryption automatically. 
- For large transfers it packages things up for efficiency. 
- The "portal" is the prettier interface. 
- BMRC want globus for the auditability. It's massive overkill for a csv, but appropriate for something the size of Biobank.
- TPSA
    - It's in the queue (John LM). Other US insitutions have already done one, so it's possible the University may accept one of those. Suspect they won't go for it. 
    - BMRC / BDI see globus as the only option. Fully expect it will go through, but globus aren't making it a prioraty to finalise the forms. 

## 2. Steps to making a decision
- Bit of development work on both
    - C-KAN: play with plugins
    - Globus portal
- Globus has all the audit functionallity, but requires TPSA which is limiting in our time frame. 
- Web interface of C-KAN or Globus would be on BMRC cloud infrastrucutre, data on BMRC Ceph.
- We need to know what the audit requirements would be. **Cass: I think with ethics committees etc., we could tell them what audit functionality we have and they could approve, rather than having them design the requirements.**
- c-kan plugin for audit (as an example): [https://github.com/ckan/ckanext-googleanalytics](https://github.com/ckan/ckanext-googleanalytics)

### C-KAN auditing
- can we implement the same thing as protocols db?
- "view" and "download" events are triggered. manually storing requst users IP addresses. 
- Could we make that a c-kan plugin? Dave to explore, ref the google analytics plugin.
- Implementation of the DUA is still a big questionmark. 


## 3. Pres to SG
- Highlight why we need this tools (why XNAT is not sufficient)
- Envisaged workflow with each ckan and globus
- how discoverable data is going to be on each
- what are the big differences between the two systems (thinking audit and authentication)
- Both options will require knowlable in-house support.
- Globus would give a better user expereince for downloading large datasets. 
- "We're providing a centralised data sharing platform"
- ORCID auth. 
- Easy to share data from XNAT (piped). Other data could be manually added.
- c-kan less development to get off the ground, globus harder to get running (TPSA etc.) but better user expereince by desktop app managing end-to-end transfer.
- **Proposal:**
    - **start with c-kan, keep an eye on download activity and need for globus. Other groups contonue to develop with globus (e.g. in TPSA and insitultional license), which we join if/when there is a need.**
- List the requirements we developed
- How they are acheived with c-kan
- indicate where globus might be an improvement
- move to globus in the future (can't do now) would give us better xyz. 
- Make it clear what we can achive for now and allow people to say that "this is not sufficient on this requirement" 



## 4. Pricing 
- Globus not terrifying, £40k pa. Will look to insitutional level licenses.
- both require us to host the data (our cost)
- Both require us to develope a portal. 
- Both will need in-house technical developer and user support




## 4. Outstanding questions which need decision making input
(e.g. acceptable requirement for external users to download a program to receive data via globus)

- We need to know which regions globus works in. Countries with sanctions against them or China.
- Globus will introduce an accessibility barrier, for example in low resource regions who do not have modern OS. C-KAN might be better for this. 


## X. Sketch out different componants of the system (use Teams whiteboard)


