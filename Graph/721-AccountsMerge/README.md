# Accounts Merge
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given a list of accounts where each element accounts[i] is a list of strings, where the first element accounts[i][0] is a name, and the rest of the elements are emails representing emails of the account. <br><br>
Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some common email to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name. <br><br>
After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails in sorted order. The accounts themselves can be returned in any order.

Example 1:

> Input: accounts = [["John","johnsmith@mail.com","john_newyork@mail.com"],["John","johnsmith@mail.com","john00@mail.com"],["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]\
Output: [["John","john00@mail.com","john_newyork@mail.com","johnsmith@mail.com"],["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]\
Explanation:\
The first and second John's are the same person as they have the common email "johnsmith@mail.com".\
The third John and Mary are different people as none of their email addresses are used by other accounts.\
We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'], \
['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.

Example 2:
> Input: accounts = [["Gabe","Gabe0@m.co","Gabe3@m.co","Gabe1@m.co"],["Kevin","Kevin3@m.co","Kevin5@m.co","Kevin0@m.co"],["Ethan","Ethan5@m.co","Ethan4@m.co","Ethan0@m.co"],["Hanzo","Hanzo3@m.co","Hanzo1@m.co","Hanzo0@m.co"],["Fern","Fern5@m.co","Fern1@m.co","Fern0@m.co"]]\
Output: [["Ethan","Ethan0@m.co","Ethan4@m.co","Ethan5@m.co"],["Gabe","Gabe0@m.co","Gabe1@m.co","Gabe3@m.co"],["Hanzo","Hanzo0@m.co","Hanzo1@m.co","Hanzo3@m.co"],["Kevin","Kevin0@m.co","Kevin3@m.co","Kevin5@m.co"],["Fern","Fern0@m.co","Fern1@m.co","Fern5@m.co"]]
 
Constraints:
- $1$ <= accounts.length <= $1000$
- $2$ <= accounts[i].length <= $10$
- $1$ <= accounts[i][j].length <= $30$
- accounts[i][0] consists of English letters.
- accounts[i][j] (for j > 0) is a valid email.

Problem can be found in [here](https://leetcode.com/problems/accounts-merge)!

## Solution
### [Solution 1](/Graph/721-AccountsMerge/solution1.py): Depth-First Search + Hash Table

```python
def accountsMerge(accounts: List[List[str]]) -> List[List[str]]:
    def DFS(email: str) -> None:
        visited_emails.add(email)
        merged_emails.append(email)

        for new_email in emails_map[email]:
            if new_email not in visited_emails:
                DFS(new_email)

    # Construct emails map for constant look-up speed
    emails_map = defaultdict(list)
    for account in accounts:
        first_email = account[1]
        for i in range(2, len(account)):
            email = account[i]
            emails_map[first_email].append(email)
            emails_map[email].append(first_email)

    # Perform DFS to merge accounts
    merged_accounts, visited_emails = [], set()
    for account in accounts:
        name, first_email = account[0], account[1]
        if first_email not in visited_emails:
            merged_emails = []
            DFS(first_email)
            merged_accounts.append([name] + sorted(merged_emails))

    return merged_accounts
```

Explanation: To merge multiple accounts, the most simple solution is to iterate for every email in each account and check if there is another account having the same email. This solution will work; however, this will result in poor time complexity. To improve the algorithm, we can first build an email map that helps us to look-up for its account in constant time (the first email are used for key in this problem). Each email in the same account are paired with the first email. In other words, we will connect emails in an account in a [star](<https://en.wikipedia.org/wiki/Star_(graph_theory)>) manner with the first email as the internal node of the star and all other emails as the leaves. After constructing the map, we can run DFS for every email we have not been visited yet. In each iteration of DFS, we mark this email as visited so that we will not need to visit it again. In addition, we will reach back to the internal node of that star with the email map we built earlier. By knowing the internal node, we can run DFS again for every unvisited email for that internal node.

Time Complexity: $O(nmlognm))$.

-   Denote $n$ as the number of accounts and $m$ as the maximum number of emails in one account. In worst case, all emails belong to one person. Therefore, sorting $n*m$ emails will need $O(nmlognm)$ time, while building emails map and running DFS both will cost $O(nm)$ time as no email will be traversed more than once. These procedures result in $O(nmlognm)$ time complexity.

Space Complexity: $O(nm)$ for emails map.

### [Solution 2](/Graph/721-AccountsMerge/solution2.py): Disjoint Set

Time Complexity: $O(nmlognm)$.

-   Denote $n$ as the number of accounts and $m$ as the maximum number of emails in one account. In worst case, all emails belong to one person. Therefore, sorting $O(n*m)$ emails will need $O(nmlognm)$ time, while building emails map and running union-find operations will cost $O(nm)$ time and $\alpha(n)$ time, respectively. Notice that $\alpha(n)$ is the inverse Ackermann function.

Space Complexity: $O(nm)$ for emails map.
