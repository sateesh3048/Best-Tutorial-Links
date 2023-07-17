Found Course without EAGER loading?
## While deleting the instructor, how was it able to get all the courses without giving "no session" error? Is it because of @Transactional annotation?

A) Yes, your understanding is correct.
When you delete an instructor, if the associated courses are fetched lazily (i.e., on-demand), 
accessing those courses outside the transactional context could lead to a "no session" error. However, 
if the deletion operation is executed within a transaction, the @Transactional annotation ensures that the session 
(database connection) is still active when fetching the courses. This allows the instructor's courses to be retrieved 
without encountering a "no session" error.

## Could not understand how course table has changed?
In AppDAOImpl class, we set the course's instructor to null but did not made any update like entityManager.update(course)
How is this possible?

A) In AppDAOImpl class, the method of deleteInstructorById is annotated with @Transaction which mean the whole block of code in deleteInstructorById  is in under **hibernate session/transaction**. In additional, the **courses object is in Persistent stage after retrieved from database**. Within in hibernate session/transaction plus  in Persistent stage, **any changes to the object will be reflected to database**.


