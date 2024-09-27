# Mission 3

## Part 0

[Link to video](https://drive.google.com/file/d/1wCCOy--9CXWEBXnovKiLMUY8UDGsRIrd/view?usp=sharing)

## Part 3

>Queries:
-- 1. Получить список юзернеймов пользователей
SELECT DISTINCT username FROM users;

-- 2. Получить количество отправленных сообщений каждым пользователем
SELECT u.username, COUNT(m.id) AS "number_of_sent_messages"
FROM messages m
JOIN users u ON m.from = u.id
GROUP BY u.username;

-- 3. Получить пользователя с самым большим количеством полученных сообщений и само количество
SELECT u.username, COUNT(m.id) AS "number_of_received_messages"
FROM messages m
JOIN users u ON m.to = u.id
GROUP BY u.username
ORDER BY COUNT(m.id) DESC
LIMIT 1;

-- 4. Получить среднее количество сообщений, отправленное каждым пользователем
SELECT u.username, AVG(message_count.cnt) AS "average_sent_messages"
FROM (
    SELECT m.from, COUNT(*) AS cnt
    FROM messages m
    GROUP BY m.from
) AS message_count
JOIN users u ON message_count.from = u.id
GROUP BY u.username;