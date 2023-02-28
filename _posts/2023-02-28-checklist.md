---
title: "Checklist for coding interviews"
date: 2023-02-28
---
During coding interviews, after you have finished your initial implementation of the question, your interviewer might ask you _"are you finished with this part?"_

Instead of saying yes immediately, try the following:
_"I think I am, but can you give me a minute to check over the code?"_

Using that minute to follow this checklist will show your interviewer you care about readability and can help you find common bugs.

1. <details>
    <summary> Choose self-describing variable and function names </summary>

    For variable names, string together 2-4 words to describe the data. For example, `activeUsers` or `indexOfMaxHeight`. I like to use variables similar to `numFoo` or `isBar` for variables representing counts and booleans, respectively. For functions, use the "verb + noun" pattern. For example, `getThing()` or `isBar()`.

    Generally, avoid single-character names like `x`, unless you use `i` as a loop index for a small (2-5 line) singly-nested loop.
    </details>

2. <details>
    <summary> Choose appropriate data structures  </summary>

    Every data structure has a prototypical element access style, query to run against the data, or both. Here is a non-exhaustive list.

    | Data structure | Traversal pattern                              | Query                                       |
    | -------------- | ---------------------------------------------- | ------------------------------------------- |
    | Queue          | Accessing the single least recently added item | -                                           |
    | Stack          | Accessing the single most recently added item  | -                                           |
    | Vector         | Accessing arbitrary elements by index          | -                                           |
    | Heap           | -                                              | What is the smallest element contained?     |
    | Map            | Access all key-value pairs in arbitrary order  | What is the value associated with this key? |
    | Set            | Accessing all elements in an arbitrary order   | Is this item in the data?                   |

    If you are accessing data from one of these data structures in a way other than the way listed in the table, you likely have chosen the wrong data structure. For example, if you only access the back of a vector and never access an element by its index, consider using a stack instead.

    Similarly, if you find yourself running a query like "is this item in the data" on a heap, consider using a set instead since membership tests are its raison-detre.
    </details>

3. <details>
    <summary> Ensure code within the same function is at the same level of abstraction. </summary>

    Consider this code:

    ```c++
    bool hasOverdueBooks(ID userId) {
        set<Loan> usersLoans = getLoansForUser(userId);
        for (const auto& loan : usersLoans) {
            string dueYear = atoi(loan.dueDate.substr(0, 4));
            string dueMonth = atoi(loan.dueDate.substr(5));
            if (dueYear < currentYear())
                return false;
            if (dueYear == currentYear() && dueMonth < currentMont())
                return false;
        }
        return true;
    }
    ```

    This code is hard for your interviewer to follow because it uses three distinct levels of abstraction in the same function. The first line speaks in the langauge of business objects - `user` and `loan` objects. The first two lines of the for-loop speak the language of string manipulation. The last four lines of the loop speak the language of date comparisons.

    Split this into three helper functions to match the three levels of abstraction.

    ```c++
    pair<int, int> parseYearAndMonth(const string& s) {
        // Code in this function uses "string" abstractions
        int year = s.substr(0, 4);
        int month = s.substr(5);
        return {year, month};
    }

    bool loanIsOverdue(const Loan &loan) {
        // Code in this function uses "date" abstractions
        pair<int, int> dueYearAndMonth = parseYearAndMonth(loan.dueDate);
        return dueYearAndMonth < make_pair(currentYear(), currentMonth());
    }

    bool hasOverdueBooks(ID userId) {
        // Code in this function uses "library" abstractions
        set<Loan> usersLoans = getLoansForUser(userId);
        return any_of(usersLoans.begin(), usersLoans.end(), loanIsOverdue);
    }
    ```

    Our new code is the same length as the old code, but can be more easily read.
    </details>

4. <details>
    <summary> Verify const-correctness </summary>

    If you can add `const` in front of variables or parameters, do so.
    </details>

5. <details>
    <summary> Trace through the parts of code similar to index + 1 </summary>

    Using `index + ` or `index - 1` is typical when accessing the previous or next element in a collection, but it is error-prone.
    </details>

6. Replace magic numbers with well-named constant variables.

7. Make sure you handle the "empty input" edge case

8. <details>
    <summary> Offer to write a few tests for your code </summary>

    If you've checked the previous seven steps items and are ready to move on, try:
    _"Should I write some tests for this function?"_

    Your interviewer would probably have asked you to write a test anyways and will appreciate your taking the initiative. Remember the acronym __ZOMBIE__ (zero, one, many, etc) when writing a comprehensive set of tests. You can learn more about that [here](https://hackernoon.com/zombie-testing-one-behavior-at-a-time-9s2m3zjo#:~:text=Pick%20Zombie%20representant,Scenarios%2C%20Simple%20Solutions).

    Some firms don't let you write tests. If you are interviewing at such a place, offer to instead trace through your code for a small input.
    </details>
