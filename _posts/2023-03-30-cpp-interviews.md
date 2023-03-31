---
title: "Why you should do programming interviews in C++"
date: 2023-03-30
---

I used Python for interviews for a few years, but in 2020, I switched to C++ and haven't looked back. Since switching to C++, I've passed interviews at major tech companies like Google and Databricks and financial firms like Jane Street and Headlands Tech GM. I attribute much of my success in passing these interviews to my choice of language.

It's conventional wisdom that you should do programming interviews in Python. The argument goes that because Python has a concise syntax and a powerful standard library, you can write solutions to interview problems faster in Python than in any other language.

This advice misses the mark. The point of interviews is not to finish the problem; it's to convince your interviewer that you would be a successful engineer at their company. From that perspective, C++ shines.

## C++ is a strongly typed language
C++ is a strongly typed language, meaning every variable has a specific data-type checked at compile-time. Writing explicit types in my code makes it easier for interviewers to follow my thought process. The fundamental issue with Python variable declarations is that when you declare a variable or function, your interviewer won't know its type, and will have a hard time determining its purpose.

Contrast these Python declarations:

```Python
index_to_range = {}
```

with this C++ declaration:

```C++
map<int, pair<int, int>> indexToRange;
```

Which variable is easier to understand? When interviewers can easily follow your thought process, you will seem more logical and competent.

Additionally, explicit types make it harder to write incorrect code. One mistake I would commonly make when writing solutions in Python was inserting the wrong type into a dictionary. Now that I use C++, this mistake seldom happens. If the shared editor used for interviews has intellisense, a red squiggle appears under incorrectly typed code, and I can fix the error. However, even without intellisense, I find it much easier to avoid mistakes if every variable declaration also includes a type.

## C++ lends you an air of seriousness
I once had an interviewer ask me to write a function to reverse a string. It took me a few seconds to write down this answer:
```Python
def reverse(s):
	return s[::-1]
```

He was not pleased with my answer. "Uh... Ok, I mean... That's right, but... Can you write that in a _real_ programming language?"

Me: "Python _is_ a real language."

Him: "I mean, a serious language... can you write it in C?"

I wrote a solution in C and passed that interview. It was unprofessional, and frankly incorrect for the interviewer to call my answer "unserious" or not "real," but this kind of disrespect for Python code is a typical attitude. The only thing unusual about this interviewer was that he was explicit about his bias.

Python's builtins and standard library functions make writing solutions to programming problems quick. However, when using these aids, you don't get to demonstrate _your_ ability to write complex, intricate, careful code. Remember: the point of interviews is __not__ to finish the problem. It is to show your interviewer you would be successful at their company.

## C++'s verbosity is not an issue when using text editors
Pre-Covid, when candidates wrote their code on a whiteboard during interviews, choosing a language other than Python for technical interviews made very little sense. However, most interviews are now conducted over Zoom via shared text editors like Coderpad.

Consider that a typical programming question may require ~20 lines of code to answer in either Python or C++. The Python code may require ~4 words per line, and the C++ code may need ~10 words per line. Assuming a typing speed of 60 words per minute, typing these solutions takes 1 minute and 20 seconds with Python and 3 minutes and 20 seconds with C++. Saving an extra 2 minutes by typing less almost never makes the difference between success and failure in the typical hour-long interview.

You can see for yourself just how little the C++ verbosity handicap matters by watching [this mock interview](https://youtu.be/EuPSibuIKIg?t=116) with competitive programmer Errichto. In the video, Errichto expertly completes a challenging interview question in ~3 minutes of C++ coding.

## C++ has somewhat obscure syntax and odd semantics
There is a running joke that Python is "just English" or "just pseudocode." In my experience, the friendliness of Python syntax makes interviewers overconfident in their ability to evaluate your code. For example, in one interview I had with Google, I wrote a Python code similar to the following:

```Python
def foo(bar: str):
    for i in range(len(bar)):
        # Do something that takes O(1) time
```

I was asked to provide the time complexity of `foo`, which is `O(N)`. My interviewer, who was not a Python programmer, insisted that the code had complexity `O(N^2)`. He believed the `len(bar)` function call took `O(N)` time and executed every loop iteration. Of course, any Python programmer knows this is not how generators work in Python, but just looking at the code, I can see how a Java or Go developer might think that.

By contrast, C++ code can simply _look_ so odd that interviewers will give you the benefit of the doubt on code you write. If they think there may be a mistake in your code, they tend to assume _your_ code is correct and that _they_ are the ones who just don't understand C++ well enough to judge your answer.

[//]: <> (One other idea I had for this post was to talk about the prior that interviewers have for seeing Python code is that it is an interviewer who will fail, and the prior for C++ code is a colleague who will succeed.)
