# SQL Query for finding hackers, who succesful solved more than one competitions tasks

## Introduction
This SQL query is designed to find the respective hacker_id and name of hackers who achieved full scores for more than one challenge

The following tables contain contest data:

- Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker; 
- Difficulty: The difficult_level is the level of difficulty of the challenge, and score is the score of the challenge for the difficulty level;
- Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge; 
- Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission.

## SQL-query
```sql
SELECT main.hacker_id, name, sucsess
FROM hackers
RIGHT JOIN (SELECT submissions.hacker_id AS hacker_id, count(*) AS sucsess
    FROM submissions
    JOIN challenges
    ON submissions.challenge_id = challenges.challenge_id
    JOIN difficulty
    ON challenges.difficulty_level = difficulty.difficulty_level
    WHERE submissions.score >= difficulty.score
    GROUP BY submissions.hacker_id
    HAVING count(*) > 1) as main
ON hackers.hacker_id = main.hacker_id
ORDER BY sucsess desc, main.hacker_id
'''
