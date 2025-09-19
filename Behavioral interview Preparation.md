### 1. Challenges I faced

**Scenario 1: Handling massive datasets without impacting browser performance**

* **The Challenge:** On a Catalogone project, we encountered a significant performance issue. We were building a feature that required loading a very long list of items, and while it worked fine with a small amount of data, the browser would slow down and eventually freeze when we had to display over a million elements. The core problem was trying to render all the elements in the DOM simultaneously.
* **What I Did:** I took the initiative to solve this performance bottleneck by creating a custom npm package. The solution leveraged the `IntersectionObserver` API to monitor the visibility of a top and bottom element in the list. This allowed me to implement a virtualized list strategy: when a user scrolled down, the observer would trigger a function to add new elements to the bottom and remove older ones from the top. The inverse would happen when a user scrolled up.
* **The Outcome:** My package ensured that at any given time, there were no more than 50 elements in the DOM, regardless of the total data size. This eliminated browser freezing and provided a smooth, seamless scrolling experience. The solution not only solved the immediate problem but also created a reusable, scalable package that could be used on other projects with large datasets, preventing similar issues in the future.


**Scenario 2: Handling a tight deadline on a complex project**

* **The Challenge:** During the development of the "Phoenix" B2B product at Amdocs, we faced a tight deadline to launch a new module that needed to generate complex JSON objects for other applications. We discovered a critical bug in the conflict resolution feature that was causing data corruption just days before the scheduled release.

* **What I Did:** I immediately initiated a rapid troubleshooting session with the team. Instead of panicking, I broke down the problem into smaller, manageable parts. I assigned specific tasks to team members based on their expertise, and I personally focused on debugging the core logic of the conflict resolution algorithm. I also communicated transparently with the project manager about the issue and our revised timeline for a fix, managing stakeholder expectations.
* **The Outcome:** Through a focused and collaborative effort, we identified the root cause of the bug within a day. We implemented a fix, thoroughly tested it, and deployed the module with only a minimal delay. This experience highlighted the importance of clear communication and a calm, methodical approach under pressure.

***

### 2. Mistakes I made in the past

**Scenario 1: Communication breakdown with a large team**

* **The Mistake:** As a Team Lead at Neosoft, I was responsible for a large-scale project involving a team of over 50 members. We were working on a complex feature that required tight coordination between different sub-teams (e.g., frontend, backend, mobile). My mistake was not establishing a formal communication channel for the team. I relied too much on informal communication channels, assuming everyone was on the same page. This led to a significant miscommunication where one sub-team built a feature based on an outdated set of API specs(Different JSON schema for response), causing a major integration roadblock and delaying the project.
* **What I Learned:** This experience taught me a crucial lesson about the scalability of communication. With a small team, informal communication can work, but with a large team, a lack of formal processes can lead to chaos. I realized that clear, documented communication is a leader's most powerful tool for ensuring alignment and efficiency.
* **How I Rectified It:** I immediately called a meeting with all the sub-team leads to address the issue. We collectively implemented a new communication protocol. We also introduced a brief daily sync-up meeting for team leads to flag any dependencies or potential roadblocks proactively. This new process streamlined our workflow and prevented similar issues on future projects.

**Scenario 2: Underestimating the complexity of a new feature**

* **The Mistake:** While working on the "Catalog One" project, I was tasked with estimating the timeline for developing the "ABAC-Enable for Product Offering" (Attribute-Based Access Control) module. The task was to create a feature that could restrict/hide elements based on the rule and role. Based on my initial assessment, I provided an aggressive timeline to the epic. However, I underestimated the complexity of implementing the ABAC foundation, which caused us to fall behind schedule.
* **What I Learned:** I learned to be more conservative with my timelines and to break down complex tasks into smaller, more detailed sub-tasks before providing an estimate. I also realized the importance of anticipating potential technical roadblocks and communicating them proactively.
* **How I Rectified It:** I owned my mistake and immediately informed the product owners of the revised timeline, providing a detailed breakdown of the remaining work and the technical challenges we encountered. This transparency helped manage their expectations and allowed us to deliver a high-quality product, even if it was a bit later than originally planned.

***

### 3. I enjoyed in a project

**Scenario 1: Building a multi-agent system**

* **What I Enjoyed:** I absolutely loved working on the "Multi-Agent-Toolcalling" project. The concept of designing a system where multiple LLMs (Large Language Models) could autonomously determine and coordinate tool calls was incredibly exciting. The project was at the cutting edge of AI.
* **Why It was Enjoyable:** It was a unique blend of front-end development (designing the UI for displaying the agents' responses) and back-end logic (developing the system that orchestrates the tool calls). The problem-solving aspect was particularly rewarding, as it felt like I was building a truly intelligent system that could reason and make decisions. I also enjoyed seeing the results of our work in real-time, as the agents responded and performed tasks.

**Scenario 2: The challenge of a real-time system**

* **What I Enjoyed:** I really enjoyed the "Human-in-Loop GenAI Integration" project. The real-time aspect of it (Socket.IO), was a thrilling challenge. It required a deep understanding of asynchronous communication and state management to ensure seamless interaction between the human user and the AI.
* **Why It was Enjoyable:** The project was not just about coding; it was about designing a system that felt responsive and intuitive. It was a perfect blend of my front-end expertise with GenAI. Building the containerized environment with Docker and Kubernetes also gave me hands-on experience with scalable, modern infrastructure, which was a new and exciting area for me. The process of seeing the system come to life and observing the seamless interaction was incredibly satisfying.

***

### 4. Leadership role in projects

**Scenario 1: Mentoring and building a large team**

* **My Role:** As a Team Lead at Neosoft, one of my most significant achievements was mentoring and developing a team of more than 50 members. My leadership wasn't just about managing tasks; it was about fostering growth and creating a strong, cohesive unit.
* **What I Did:** I implemented a mentorship program where senior developers were paired with junior members. I also introduced weekly knowledge-sharing sessions where team members could present on a new technology or a challenging problem they solved. I focused on empowering my team by delegating responsibilities and trusting their abilities.
* **The Outcome:** This approach not only improved the team's overall skill level and productivity but also boosted morale and reduced turnover. I'm proud that many of the developers I mentored went on to take on leadership roles themselves.

**Scenario 2: Leading pre-sales and client interactions**

* **My Role:** As a Team Lead, I was responsible for leading many projects from the pre-sales stage all the way to completion. This included direct interaction with clients for requirement gathering and solution architecting.
* **What I Did:** During pre-sales activities, I would meet with potential clients to understand their needs and propose a technical solution. For a project involving a web and mobile application, I listened to the client's business goals and then architected a full-stack solution using React for the front-end and Node.js for the back-end and we will wrap the application in Electron for mobile application. I created a detailed technical proposal and a proof of concept (POC) to demonstrate the feasibility of our solution.
* **The Outcome:** My ability to translate business requirements into a clear technical roadmap and my hands-on experience with the technologies gave the client confidence in our team. We won the project and successfully delivered a solution that not only met their initial needs but also exceeded their expectations in terms of performance and scalability.

***

### 5. Conflicts in projects with colleagues

**Scenario 1: Disagreement on a technical approach**

* **The Conflict:** On the "KnowledgeOne" project, a colleague and I had a disagreement about the best way to integrate Confluence with the LLM. I proposed using a RAG (Retrieval-Augmented Generation) system with Pinecone as the vector database, as I believed it was the most efficient and scalable solution for our embedded data storage. My colleague, however, preferred a different approach using a simpler, more traditional database, arguing it would be faster to implement.
* **How I Handled It:** I listened carefully to my colleague's reasoning and acknowledged their point about the faster implementation time. However, instead of simply dismissing their idea, I presented a more detailed analysis of the long-term benefits of the RAG system, highlighting its scalability and the improved accuracy it would provide by retrieving information from our large Confluence knowledge base. I also offered to build a small prototype of my proposed solution to demonstrate its effectiveness.
* **The Outcome:** My colleague appreciated the data-driven approach and the effort to build the prototype. After seeing the clear benefits of the RAG system, they agreed it was the better long-term solution. We moved forward with my proposed architecture, and the project was a success.

**Scenario 2: The classic "backend vs. frontend" conflict**

* **The Conflict:** During the development of the "Phoenix" B2B product, there was a miscommunication between the frontend and backend teams regarding the format of a JSON object. The backend team had changed the structure of the JSON object without informing us on the frontend team, which caused our module to fail. My front-end colleagues were frustrated, and we were behind schedule.
* **How I Handled It:** As a senior developer, I took the initiative to bridge the communication gap. I scheduled a quick meeting with the Lead and the relevant developers. I calmly explained the issue and suggested that we create a Confluence page where all changes to the API and JSON structures would be logged and communicated in real-time. This would prevent similar issues in the future.
* **The Outcome:** The backend team was receptive to the idea. We implemented a new process of using a collaborative tool to document all API changes, which significantly improved our team's communication and efficiency. This experience reinforced the importance of proactive communication and process improvement in a collaborative environment.

Here is a different scenario for the same question, this time drawing from your experience as a Team Lead at Neosoft.

***

**Scenario 3: Team Member with a highly creative problem-solver who preferred to "just get it done," often bypassing our standard documentation and code review processes**

**The challenge** undocumented code caused integration issues for other developers on the project. My task was to address this without impacting their creative energy, which was a huge asset to the team.

- I handled this by first scheduling a one-on-one meeting to understand their perspective. 
- I acknowledged their incredible speed and skill, recognizing that my personality might be too focused on process for their liking. Then, I explained the **"why"** behind our team standards: with a team of our size, clean code and clear documentation were not just a preference but a necessity for long-term project health and maintainability.

***

### 6. What I did differently apart from my org roles

**Scenario 1: Self-learning and skill expansion**

* **The Action:** I have a strong passion for continuous learning that goes beyond my daily responsibilities. While working as a front-end developer, I made the conscious decision to expand my expertise into Generative AI and machine learning. This wasn't a requirement of my job at the time; it was a personal goal.
* **How it was Different:** I dedicated my personal time to studying neural networks, lang graph, lang chain. I enrolled in online courses, read research papers, and worked on personal projects to get hands-on experience. This self-driven learning allowed me to become proficient in a new domain.
* **The Outcome:** This independent learning proved to be a major advantage. It directly led to me being able to contribute to innovative projects like the "Human-in-Loop GenAI Integration" and the "Multi-Agent-Toolcalling" system at Amdocs, which were outside the scope of a typical front-end developer's role.

**Scenario 2: Developing side projects to explore new technologies**

* **The Action:** I've always been a strong believer in building personal projects to apply what I learn. While working on enterprise applications, I decided to build an npm package that will handle a true infinite loader, without freezing the browser.
* **How it was Different:** I faced lot of challenges to work on the details of the npm package, I read many articles, and I went very deep into how browser trace interaction works, which has more priority than all. But eventually, I did the npm package.
* **The Outcome:** I have the npm package published, and I used in one of our internal projects. It worked very well.


## Q. What keyword did your senior and junior colleges use for you?

### Key Takeaway for Your Answer

### What Juniors Would Say 🧑‍💻

* **Keywords:** **Helpful, Patient, Mentor, Go-to Person, Knowledgeable**

* **Example Answer:** "I believe my junior colleagues would describe me as the **'go-to person'** on the team. They would say I'm **patient** and always willing to help. For example, a few months ago, a new developer on my team was struggling with a complex scenario with a thunk action in Redux. Instead of just giving them the solution, I sat with them, explained the underlying principles of the thunk action, and walked them through the debugging process. The goal wasn't just to fix the bug, but to help them understand the 'why' behind the code. I believe they would describe me as a **mentor** who invests in their growth."

---

### What Senior People Would Say 👩‍💼

* **Keywords:** **Reliable, Strategic, Problem-Solver, Proactive, Owner**

* **Example Answer:** "My senior colleagues and managers would likely describe me as **'strategic'** and a **'problem-solver'**. They would say that I am someone who doesn't just write code, but also thinks about the long-term impact on the product and the business. 

- For instance, on our last project, I noticed a recurring performance issue caused by inefficient data fetching on the front-end. It wasn't my assigned task, but I proactively investigated it. In the UI component, it was being re-rendered multiple times. I added React.Memo and useCallbacks for optimising the re-renders. This improved our page load times by over 30%. They would describe me as an **'owner'** who takes responsibility for the success of the entire feature."

## Introduce Yourself

- I'm a passionate and results-driven Front-End Developer with 10 years of experience building high-performance, scalable applications. My core expertise lies in modern technologies like **React, Redux Toolkit, and TypeScript**, which I've used to deliver complex projects throughout my career.

- In my current role at Amdocs, I am an Advanced Software Developer working on an enterprise catalog project.
- A key challenge I successfully solved was optimizing a massive data list, where I developed a custom npm package that prevented browser freezing by dynamically rendering only a handful of elements at any given time, ensuring a smooth user experience.

- Before that, as a Team Lead at Neosoft, I not only worked hands-on with a wide range of technologies like **React, React-Native, and Node.js, Ionic, Angular**, but I also mentored and grew a team of over 50 members. I was directly involved in pre-sales activities and client interactions, where I'd architect and lead end-to-end project solutions.

- I'm now expanding my skills into **Generative AI and machine learning**. My recent projects, like the **Multi-Agent-Toolcalling** and **KnowledgeOne** systems, allowed me to apply this knowledge by leveraging multiple LLMs and RAG systems.

I am now seeking a fast-paced and innovative environment where I can leverage my deep front-end expertise and growing knowledge in AI to build the next generation of applications, like yours.
