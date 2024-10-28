# tds-proj1

**Objective:** Perform analytics on GitHub users and repositories for a selected city.

## Methodology for Collecting Data

1. Initially, I considered using the GitHub Users API. To familiarize myself with the data, I conducted a trial run by making a simple GET request in my browser (using Chrome's Pretty Print option). For the city of Chennai, I discovered there are **423 users** with a follower count greater than **50**.
  
2. However, I realized that the Users API alone would not provide all the necessary data for this project. To retrieve details such as email addresses, locations, and the repositories users are following, I would need to make an initial API call to obtain the list of users (in this case, **423 users**), followed by individual API calls for each user. This would result in an additional **423 calls**, assuming no server-side issues arise that would require re-running the scraping program.

3. After reviewing the GitHub API rate limits, I found that there is a cap of **60 requests per hour**. My calculations indicated that retrieving user data alone would take more than **4 hours** (fetching the first **60 user details**, waiting for another hour, and then resuming from where I left off). While this approach was feasible, it was highly inefficient. I verified on the Discourse forum that the project parameters (specifically the user count) indeed allow for all information to be retrieved within **60 requests**.

4. **Exploring GraphQL as a Solution:** I investigated GraphQL, which GitHub provides for more efficient access to user data.

5. Before coding the scraping program in Python, I aimed to gain experience with GraphQL queries in the context of this project. I fine-tuned my queries on a limited dataset (restricting the output to **10 records** to verify the query structure and node relationships). The GitHub GraphQL Explorer's IntelliSense feature was particularly helpful in ensuring I used the correct field names. It’s important to note that a personal access token (PAT) is required for this tool. Once I validated the GraphQL query with limited output, I transferred it into the Python program.

6. **Testing the First Iteration:** I realized that while the query executed successfully, the program stopped halfway through printing the results to the console.

