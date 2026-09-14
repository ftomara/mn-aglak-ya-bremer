## Deep Dives:
  - First when we designing the system we choose the priority of the system
    is to be consistent as it's important when a user come and apply for a job 
    to have the last updated stauts , so candidates can see which jobs is still
    accepting requests and which has been closed, so we can get good UX 
    experience.
  
  - And how the system should handle more and more users?
    the solution is the system has to be scalable to handle all the read and writes
    efficiently and it will handle all these users by using a load balancer which tries 
    to make our system more efficient. 
  
  - But what if the system or a service goes down?
    here we comes to availability. since, the system has to handle millions of users
    per day , it's expected that the services can go down, so here comes availability
    so we can do this by making copies of our data on different nodes so even if 
    the service goes down on a node, we can shift to the standby node without 
    making the users that something wrong has happened.
  
  - But how to make our system fast as we serve millions every day?
    the answer here is to make the system works with low latency, so
    we made a cache which has the most popular jobs that people has
    searched for, which make the process of searching more efficient so
    we can get the search results <300ms.  
  
  - So how the candidate will know that he matched for a job?
    After the candidate makes an account he will make a match
    by using (match service) and then the match service goes to
    (job service) to get jobs then match the jobs with condidate 
    skills in (matching service) return list of matched jobs to the 
    candidate.
  
  - When the Candidate search , how the request can be handled?
    when the candidate search for jobs, we use pagination technique
    so, it comes with 20 job per request.  

  

  
