# SQL Query for finding hackers, who succesful solved more than one competitions tasks

## Introduction
This SQL query is designed to find the respective hacker_id and name of hackers who achieved full scores for more than one challenge

The following tables contain contest data:

- Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker; 
- Difficulty: The difficult_level is the level of difficulty of the challenge, and score is the score of the challenge for the difficulty level;
- Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge; 
- Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission.

# SQL-query
'''
select main.hacker_id, name, sucsess
from hackers
right join (select submissions.hacker_id as hacker_id, count(*) as sucsess
    from submissions
    join challenges
    on submissions.challenge_id = challenges.challenge_id
    join difficulty
    on challenges.difficulty_level = difficulty.difficulty_level
    where submissions.score >= difficulty.score
    group by submissions.hacker_id
    having count(*) > 1) as main
on hackers.hacker_id = main.hacker_id
order by sucsess desc, main.hacker_id
'''
