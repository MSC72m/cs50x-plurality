# Plurality Voting System

## Project Description
This project is a solution to a CS50x problem set that involves implementing a plurality voting system. The program allows users to vote for candidates and determines the winner based on who receives the most votes. If there's a tie, all winners with the highest vote count are displayed.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Code Explanation](#code-explanation)

## Installation
No special installation is required for this project. 

## Usage
To compile and run the project, use the following commands:
make plurality
./plurality candidate1 candidate2 ... candidateN
You will be prompted to enter the number of voters and then to cast votes for candidates.

## Code Explanation
Constants and Structures

``` C
#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max number of candidates
#define MAX 9

// Candidates have name and vote count
typedef struct
{
    string name;
    int votes;
} candidate;

// Array of candidates
candidate candidates[MAX];

// Number of candidates
int candidate_count;
```
#include <cs50.h>, #include <stdio.h>, and #include <string.h> include the necessary libraries for CS50 functions, standard input/output functions, and string handling functions respectively.
#define MAX 9 sets the maximum number of candidates to 9.
typedef struct defines a structure for a candidate with a name and votes.
candidate candidates[MAX] declares an array to hold the candidates.
int candidate_count holds the number of candidates.
Function Prototypes

``` C
bool vote(string name);
void print_winner(void);
bool vote(string name); is the prototype for the function that updates vote totals given a new vote.
void print_winner(void); is the prototype for the function that prints the winner(s) of the election.
Main Function

``` C
int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: plurality [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX)
    {
        printf("Maximum number of candidates is %i\n", MAX);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i].name = argv[i + 1];
        candidates[i].votes = 0;
    }

    int voter_count = get_int("Number of voters: ");

    // Loop over all voters
    for (int i = 0; i < voter_count; i++)
    {
        string name = get_string("Vote: ");

        // Check for invalid vote
        if (!vote(name))
        {
            printf("Invalid vote.\n");
        }
    }

    // Display winner of election
    print_winner();
}
``` 
if (argc < 2) checks if there are enough command-line arguments (at least one candidate) and prints usage instructions if not.
candidate_count = argc - 1; sets the number of candidates.
if (candidate_count > MAX) checks if the number of candidates exceeds the maximum allowed and prints an error message if true.
The for loop populates the candidates array with candidate names and initializes their vote counts to zero.
int voter_count = get_int("Number of voters: "); prompts the user to enter the number of voters.
The second for loop iterates over each voter, prompting them to enter a candidate name. If vote(name) returns false, it prints "Invalid vote.".
print_winner(); displays the winner of the election.
Vote Function
``` C
bool vote(string name)
{
    for (int i = 0; i < candidate_count; i++)
    {
        if (strcmp(candidates[i].name, name) == 0)
        {
            candidates[i].votes++;
            return true;
        }
    }
    return false;
}
```
The for loop iterates over each candidate.
if (strcmp(candidates[i].name, name) == 0) checks if the given name matches a candidate's name.
If a match is found, the candidate's vote count is incremented and the function returns true.
If no match is found, the function returns false.
Print Winner Function
``` C
void print_winner(void)
{
    int max_vote = 0;
    for (int i = 0; i < candidate_count; i++)
    {
        if (max_vote < candidates[i].votes)
        {
            max_vote = candidates[i].votes;
        }
    }
    for (int i = 0; i < candidate_count; i++)
    {
        if (candidates[i].votes == max_vote)
        {
            printf("%s\n", candidates[i].name);
        }
    }
}
```
int max_vote = 0; initializes the maximum vote count to zero.
The first for loop finds the highest vote count among the candidates.
The second for loop prints the names of all candidates who have the maximum vote count, handling ties by printing each winner.
