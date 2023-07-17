Found Course without EAGER loading?
## While deleting the instructor, how was it able to get all the courses without giving "no session" error? Is it because of @Transactional annotation?

A) Yes, your understanding is correct.
When you delete an instructor, if the associated courses are fetched lazily (i.e., on-demand), 
accessing those courses outside the transactional context could lead to a "no session" error. However, 
if the deletion operation is executed within a transaction, the @Transactional annotation ensures that the session 
(database connection) is still active when fetching the courses. This allows the instructor's courses to be retrieved 
without encountering a "no session" error.
