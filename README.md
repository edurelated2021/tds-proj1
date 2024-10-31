# Tools in Data Science Project 1
Student id: 24ds3000100

## Project objective:
For a given city, scrape details of popular Github committers and their code repositories. Perform analytics on the retrieved data to find interesting insights and patterns with an aim to frame actionable recommendations.

## Methodology for scraping the data
**In summary:**
1. Explored both the Github REST api (classic variant) as well the GraphQL variant. Decided to use the GraphQL variant because that would be efficient in terms of reducing the number of calls required significantly (this is particularly important when we scale out).  In fact, using the GraphQL variant, the entire user details data (with the required filters) can be retrieved within a minute.
2. Performed a few basic data transformations (such as removal of special characters, converting nulls to spaces etc.) on the incoming data.
3. Saved the two csv files and performed analysis on them.

**Softwares/tools used:**
1. Initial data exploration: Chrome browser (with pretty print turned on)
2. Environment/Program: Python (Google Colab notebook) and associated Python libraries
3. Additional tools: [Github GraphQL Explorer](https://docs.github.com/en/graphql/overview/explorer) [for performing tests with a restricted input size and then debugging the GraphQL queries], Notepad++, Libre Office, Google Sheets, ChatGPT 4o mini 

**Details:**
1. Initially, I considered using the classic variant of the GitHub Users API. To order to become familiar with the fields, I did a few trial runs by invoking the endpoints directly on my web browser (with Chrome's Pretty Print option turned on for easy readability). For the city of Chennai, found there are **423 users** with a follower count greater than **50**.  
2. However, realized that the Users API alone will not provide all the necessary user details required for this project. To retrieve additional details such as email address, locations, the number of repositories users are following, I would need to, first, make an initial API call to obtain the list of users (for the city of **Chennai** there are **423 users**), followed by API calls to fetch additional data associated with each individual user (one api call per user). This would result in an additional **423 calls**, assuming no server-side issues arise during execution that would otherwise require re-running the scraping program.
3. Explored GraphQL as an alternate solution over the classic REST variant. Unlike the classic variant where one need to invoke an initial service to retrieve the list of users and then iterate over the list of users and fire one REST call per user to fetch the user details, the GraphQL variant allows to 'merge' these separate invocations into a single GraphQL construct. The efficiencies gained on the User details fetch is significant as my tests showed the entire set of user details were retrieved and the users.csv file being generated well under a minute.
4. With regards to the repositories details, invoked another GraphQL query (one per user) and created the repositories.csv file.
5. Created a Personal Access Token (PAT) and used that in the authorization headers while invoking the GraphQLs. A PAT not only increases the number of invocations allowed per hour, but also allows retrieval of some fields (such as email ids) in cleartext form which otherwise will be scrubbed in the unauthenticated calls.
6. Before coding the scraping program in Python, debugged and made adjustments to the GraphQL queries using the GitHub GraphQL Explorer (a personal access token is required) on a limited dataset (restricted the resultset size to 10 records for test purposes to verify the query structure and node relationships). The GitHub GraphQL Explorer's IntelliSense feature was helpful in zeroing in to the correct field names. Once I validated the GraphQL queries, I transferred them over to the Python program.
7. Used a few basic data transformations (special characters removal, converting nulls to spaces etc. per the project description) from the incoming data.
8. Ran the program in Google Colab environment and generated the users.csv and repositories.csv files to perform further analysis on.

## Interesting and surprising facts I found after analyzing the data
1. A _textual analysis_ of the developer bios reveal a few interesting facets:
   - **Human-Centric Values**: Many developers express values related to creativity, problem-solving, and making a positive impact through technology. Phrases about passion, love for coding, and community engagement highlight a human-centric approach to technology.
   - **Soft Skills**: There is a notable emphasis on communication, mentorship, and collaboration, essential skills in today’s tech environment, indicating that technical expertise is complemented by strong interpersonal abilities.
   - **Hackathons and Competitions**: Many developers have engaged in hackathons, suggesting a vibrant culture of innovation and competition that drives developers to refine their skills and showcase their work.
2. There is a significant spike in the number of users who registered on Github in the year of the covid e.g. 2020
   ![2020 spike!](/images/numberOfUsersByYear.jpg)  
   This spike in the number of new GitHub users in 2020 was largely driven by the COVID-19 pandemic, which shifted many to work remotely and increased the need for digital collaboration tools. As people sought to learn new skills while at home, interest in programming and open-source software grew, leading to more individuals creating GitHub accounts. The rise of _online_ coding courses and bootcamps also contributed to this trend, as learners needed platforms to share their work. Additionally, many organizations accelerated their digital transformation efforts, further boosting the use of GitHub for project collaboration.
3. **Bursts some popular myths/preconceived notions:**
   **Myth**: That having a high number of repositories and/or longer bio will attract more followers.
   **Fact**: In fact a significant number of the popular github users (measured in terms of number of followers) had a respositories count in double digits/shorter bios.
   



## Actionable recommendation for developers based on data analysis


## Notes to myself (beyond the scope and requirements for this project)
1. Does the most popular languages depend on the geographies? Perhaps it does. For example, consider the prevelance of Kotlin in East European nations. A geographical visualization using a tool such as Tableau (say, using a world map and plotting the most prevalant programming language in prominent cities worldwide) can be a good and useful visualization. This will require a scan of Github metadata across several cities.

