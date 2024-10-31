# Tools in Data Science Project 1

## Project objective:
For the city of Chennai, India scrape details of popular Github committers and their code repositories. Perform analytics on the retrieved data to find interesting insights and patterns with an aim to frame actionable recommendations. 

## Methodology for scraping the data
**In summary:**
1. For retrieving users and repositories information, explored Github REST api (classic variant) as well the GraphQL variant. Decided to use the GraphQL variant because that would be efficient in terms of reducing the number of calls significantly (this is particularly important when we scale out).  In fact, using the GraphQL variant, the entire user details data (with the required filters) can be retrieved within a minute.
2. Performed a few basic data transformations (such as removal of special characters, converting nulls to spaces etc.) on the incoming data.
3. Saved the two csv files and performed analysis on them.

**Softwares/tools used:**
1. Initial data exploration: Chrome browser (with pretty print turned on)
2. Environment/Program: Python (Google Colab notebook) and associated Python libraries
3. Additional tools: [Github GraphQL Explorer](https://docs.github.com/en/graphql/overview/explorer) [for performing tests with a restricted input size and then debugging the GraphQL queries], Notepad++, Libre Office, Google Sheets, ChatGPT 4o mini 

**Details:**
1. Initially, I considered using the classic variant of the GitHub Users API. To order to become familiar with the fields, I did a few trial runs by invoking the endpoints directly on the web browser (with Chrome's Pretty Print option turned on for easy readability). For the city of Chennai, I found there are **423** users with a follower count greater than **50**.  
2. However, realized that the Users API alone will not provide all the necessary user details required for this project. To retrieve additional details such as email address, locations, the number of repositories users are following, I would need to, first, make an initial API call to obtain the list of users (for the city of **Chennai** there are **423** users), followed by API calls to fetch additional data associated with each individual user (one api call per user). This would result in an additional **423** calls, assuming no server-side issues arise during execution that would otherwise require re-running the scraping program.
3. Explored GraphQL as an alternate solution over the classic REST variant. Unlike the classic variant where one need to invoke an initial service to retrieve the list of users and then iterate over the list of users and fire one REST call per user to fetch the user details, the GraphQL variant allows to 'merge' these separate invocations into a single GraphQL construct. The efficiencies gained on the User details fetch is significant as my tests showed - the entire set of user details were retrieved and the users.csv file was generated in under a minute.
4. With regards to the repositories details, invoked another GraphQL query (one per user) and created the repositories.csv file.
5. Created a Personal Access Token (PAT) and used that in the authorization headers while invoking the GraphQLs. A PAT not only increases the number of invocations allowed per hour, but also allows retrieval of some fields (such as email ids) in cleartext form which otherwise will be scrubbed in the unauthenticated calls.
6. Before coding the scraping program in Python, debugged and made adjustments to the GraphQL queries using the GitHub GraphQL Explorer (a personal access token is required) on a limited dataset (restricted the resultset size to 10 records for test purposes to verify the query structure and node relationships). The GitHub GraphQL Explorer's IntelliSense feature was helpful in zeroing in to the correct field names. Once I validated the GraphQL queries, I transferred them over to the Python program.
7. Used a few basic data transformations on the raw retrieved data (special characters removal, converting nulls to spaces etc. per the project description).
8. Ran the program in Google Colab environment and generated the users.csv and repositories.csv files to perform further analysis on.

## Interesting and surprising facts I found after analyzing the data
1. A _textual analysis_ of the developer bios in Chennai revealed a few interesting facets:
   - **Human-Centric Values**: Many developers express values related to creativity, problem-solving, and making a positive impact through technology. Phrases about passion, love for coding, and community engagement highlight a human-centric approach to technology.
   - **Soft Skills**: There is a notable emphasis on communication, mentorship, and collaboration, essential skills in today’s tech environment, indicating that technical expertise is complemented by strong interpersonal abilities.
   - **Hackathons and Competitions**: Many developers have engaged in hackathons, suggesting a vibrant culture of innovation and competition that drives developers to refine their skills and showcase their work.
2. There is a significant spike in the number of users who registered on Github in the year of the covid e.g. 2020
   ![2020 spike!](/images/numberOfUsersByYear.jpg)  
   This spike in the number of new GitHub users in 2020 was largely driven by the COVID-19 pandemic, which shifted many to work remotely and increased the need for digital collaboration tools. As people sought to learn new skills while at home, interest in programming and open-source software grew, leading to more individuals creating GitHub accounts. The rise of _online_ coding courses and bootcamps also contributed to this trend, as learners needed platforms to share their work. Additionally, many organizations accelerated their digital transformation efforts, further boosting the use of GitHub for project collaboration.
3. **Dispels some popular myths/misconceptions/assumptions/preconceived notions:**    
   **Myth**: _That having a high number of repositories and/or longer bio will attract more followers._  
   **Fact**: In fact a significant number of the popular github users (measured in terms of number of followers) had a respositories count in double digits/shorter bios. In other words, users follow to indicate their appreciation towards quality and usefulness of the projects.  
   **Myth**: _The more the watchers for a given code repository, the more the number of stargazers (people who find the code repository useful)._   
   **Fact**: The correlation is rather weak indicating that github users star a given repository as a way to show appreciation or bookmark a project for future reference (without _neccessarily_ becoming followers of the project).
4. **JavaScript** is the most popular language.
JavaScript's popularity stems from its versatility, being essential for web development and enabling interactive features on websites. The rise of frameworks and libraries like React, Angular, and Vue.js has further enhanced its capabilities and ease of use. Additionally, the growth of Node.js has allowed JavaScript to be used for _server-side_ development, enabling full-stack applications with a single language. Its large community and extensive resources also contribute to its widespread adoption.



## Actionable recommendation for developers based on data analysis
Point 3 in the findings (please refer above) indicate that there is a significant weightage given to quality over quantity and more is not necessarily better. Quality and utility of the work product, in turn directly impacts the visibility and user engagement. 
1. Developers should focus on the quality of their outputs. Following are a few suggestions:
- **Create Quality Projects**: Focus on well-documented, useful projects that solve real problems to attract interest.
- **Maintain high code quality**: Code reviews, automated code linting, following secured coding standards, creating unit tests are some of the recommendations to ensure high quality of the code
- **Maintain two Github accounts**: I would suggest segregating high quality production grade open source code in the primary user account (the account one wishes to showcase to the community) and add any 'proof-of-concept', 'bootcamp'/practice grade code (for newer technologies that the developer is currently learning) in a separate practice account. As the data analysis shows, there is a definite preference of quality over quantity, fewer but high quality projects in the primary account will lead to distraction free, focussed and meaningful engagement from the community (a side result of which will be an increase in the number of followers/stargazers).
- **Engage with the Community**: Participate in discussions, comment on issues, and contribute to other repositories to build connections.
- **Consistent Updates**: Regularly update projects with new features, bug fixes, or improvements to keep followers engaged.
- **Collaborate on Open Source**: Join open source projects and collaborate with other developers to enhance visibility and credibility.
- **Write Tutorials and Blogs**: Share your knowledge through articles or tutorials that showcase your projects or concepts, linking back to your GitHub profile/repositories.
- **Optimize Your Profile**: Ensure your GitHub profile is complete and showcases your best work, making it easier for users to follow you.
2. Focus on current trends/upskill yourself with the current state of the art:  
  Data analysis indicates strong prevelance of frontend technologies (Javascript) and also a growing usage of Python (primarily in the domain of machine learning) as two of the most popular languages. Developers should upskill themselves on these technologies in keeping up with the trend and needs of the industry. 

## Notes to myself (beyond the scope and requirements for this project)
1. Does the most popular languages depend on the geographies? Perhaps it does. For example, consider the prevelance of Kotlin in East European nations. A geographical visualization using a tool such as Tableau (say, using a world map and plotting the most prevalant programming language in prominent cities worldwide) can be a good and useful visualization. This will require a scan of Github metadata across several cities.
2. Explore this question: Do developers who are working in the field of machine learning also necessarily learning frontend technologies? What is the correlation? A cross geography scan will be ideal because trends may emerge in Silicon Valley and gradually be noticeable in other geographies with the passage of time.

