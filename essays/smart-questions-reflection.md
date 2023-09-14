---
layout: essay
type: essay
title: "Smart questions"
# All dates must be YYYY-MM-DD format!
date: 2023-09-05
published: true
labels:
  - Questions
  - Answers
  - StackOverflow
---

<img width="300px" class="rounded float-start pe-4" src="../img/smart-questions-reflection/questions.jpg">

## "Smart" questions === "smart" answers.

I assume that it is obvious to all of us that when we ask thought-provoking questions we get thoughtful answers. Personally, I have had experiences when I was not satisfied with answers, not because they were bad, but because I didn’t ask the “right” questions or “right” sources. This essay is about asking “smart” questions for software engineers, particularly in forums like StackOverflow, so I will try to evolve the essay around it. Software engineering is a collaborative field, so it’s vital to know how to ask “good” questions and who to ask. It not only makes you look competent, but it also allows others to understand your problem better and help you find a solution more efficiently. Let’s consider the process of formulating “smart” programming questions and the important steps to take before it.

No one likes to answer obvious questions, which already have answers, because it wastes time on both ends, so it is important to do research before asking one. In the case of programming, the first thing that we should go to is the web. It seems so obvious, that mentioning it seems redundant, but so often people are not willing to use the internet and instead ask someone for help. Hence, it is important when asking a question to display the fact that you did research and what you have learned from it. I think it would be better if I explain the contrast between “smart” and “not-smart” questions by using examples, that I found in StackOverflow.


## "Smart" question.

Here is a link to [Smart question](https://stackoverflow.com/questions/11227809/why-is-processing-a-sorted-array-faster-than-processing-an-unsorted-array)

Once I opened this question, I thought to myself, “Finally, that’s the question I’ve been looking for.” It looked professional just at first glance, important words are highlighted and paragraphs are structured in a meaningful sequence, revealing the story behind the question. The question, “Why is processing a sorted array faster than processing unsorted?” is thought-provoking and advanced, just what “hackers” are looking for. In the “Background”, the author explains his observations about the time difference of running the code with sorted and unsorted arrays in a primary loop. The author tested the case in C++ and Java to eliminate the possibility that the phenomenon occurs in a particular language only. The author's attempts show that he has done some work before he addressed the public forum. The question is stated clearly and source code from his test is provided. The author is using a professional language that takes readers straight to the point. Unsurprisingly, this question attracted many interesting answers from developers. It is one of the highest-rated questions in StackOverflow.

```
In this C++ code, sorting the data (before the timed region) makes the primary loop ~6x faster:

#include <algorithm>
#include <ctime>
#include <iostream>

int main()
{
    // Generate data
    const unsigned arraySize = 32768;
    int data[arraySize];

    for (unsigned c = 0; c < arraySize; ++c)
        data[c] = std::rand() % 256;

    // !!! With this, the next loop runs faster.
    std::sort(data, data + arraySize);

    // Test
    clock_t start = clock();
    long long sum = 0;
    for (unsigned i = 0; i < 100000; ++i)
    {
        for (unsigned c = 0; c < arraySize; ++c)
        {   // Primary loop.
            if (data[c] >= 128)
                sum += data[c];
        }
    }

    double elapsedTime = static_cast<double>(clock()-start) / CLOCKS_PER_SEC;

    std::cout << elapsedTime << '\n';
    std::cout << "sum = " << sum << '\n';
}
Without std::sort(data, data + arraySize);, the code runs in 11.54 seconds.
With the sorted data, the code runs in 1.93 seconds.
(Sorting itself takes more time than this one pass over the array, so it's not actually worth doing if we needed to calculate this for an unknown array.)

Initially, I thought this might be just a language or compiler anomaly, so I tried Java:

import java.util.Arrays;
import java.util.Random;

public class Main
{
    public static void main(String[] args)
    {
        // Generate data
        int arraySize = 32768;
        int data[] = new int[arraySize];

        Random rnd = new Random(0);
        for (int c = 0; c < arraySize; ++c)
            data[c] = rnd.nextInt() % 256;

        // !!! With this, the next loop runs faster
        Arrays.sort(data);

        // Test
        long start = System.nanoTime();
        long sum = 0;
        for (int i = 0; i < 100000; ++i)
        {
            for (int c = 0; c < arraySize; ++c)
            {   // Primary loop.
                if (data[c] >= 128)
                    sum += data[c];
            }
        }

        System.out.println((System.nanoTime() - start) / 1000000000.0);
        System.out.println("sum = " + sum);
    }
}
With a similar but less extreme result.

My first thought was that sorting brings the data into the cache, but that's silly because the array was just generated.

What is going on?
Why is processing a sorted array faster than processing an unsorted array?
The code is summing up some independent terms, so the order should not matter.
```

## "Not smart" question.

Here is a link to [Not smart question](https://stackoverflow.com/questions/75661013/we-are-using-epson-xamarin-android-package-and-getting-error-after-run-exception)

In contrast to the previous paragraph, I want to show an example of what a “not smart” question looks like. The author is experiencing issues with his “Epson” printer and instead of addressing this question directly to the company, which specializes in the hardware and certainly has support for owners of their products, he asks for help in the forum for programmers, StackOverflow. Furthermore, the problem he is having is some kind of exception after running the source code, but he doesn’t provide any background information, what he is trying to achieve is not clear at all. The author seems to be unwilling to take any steps himself and strongly relies on others. The comment that the author makes under his problem is a good assertion for the last sentence, “Please any one having update on this it will help us lot. Thanks in advance."From the author's writing and name, I can deduce that English is probably not his native language, but it doesn’t justify his unprofessional question formulation. There are many internet tools that can help enhance grammar, and it is almost unforgivable to write like this. English is also not my first language and I am still learning it, but if I would write a sentence like this to my professor, what would he think of me? At best, he will think that I am careless and just don't show him my respect. The same can be said about the author of this question, that he is not taking time to formulate a “good” question and check his grammar, which shows his unprofessionalism and indifference to the community of people in StackOverflow, many of whom are professionals. His question was published at the beginning of March this year and the only comment he got was “Shouldn't Epson have its own documentation to help you with this?” Some may think that it is rude to say that. It is, but wasn’t it rude to ask an inappropriate question and show a lack of respect to the readers?

```
Q: We are using Epson.Xamarin.Android package and getting error after Run Exception of type 'Epson.Xamarin.Android.Epos2.Epos2Exception' was thrown

var printer = new Printer(Serie.TmM30, Model.Chinese, BaseContext);
printer.Connect("192.168.2.11", 9100);                 printer.AddText("Hello, world!\n");
printer.AddText("This is a sample text.\n");
printer.AddText("Thank you for using Epson printers.\n");                 
printer.SendData(200);
printer.Disconnect();
Using Above code compile an run successfully but getting Exception of type 'Epson.Xamarin.Android.Epos2.Epos2Exception' was thrown.
```


## Conclusion

In conclusion, I made myself sure again that the quality of a response is directly proportional to the quality of a question and how appropriate it is being addressed. Answering the question is work, asking a question must also be work so that it is performed in an efficient manner for both ends.
