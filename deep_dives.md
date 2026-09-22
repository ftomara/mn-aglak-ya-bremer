## Deep Dives:
- Designing system like this actually the first thing we
  should think about is scalability as the system can scale
  to handle more users, orders and robots and so on

- How the system shall solve problems like robot failure?
  here the answer is resilience which help the system to be 
  more effecient as even if the robot failed the customer's
  order doesn't get affected and the order arrives to the 
  customer in the estimated time. and we can achieve this
  when the robot fails it will notify the system. then the 
  system will search for the nearest available robot to take 
  his place. if there is no robots so we will delay the order
  and notify the customer that it will be delayed for a little
  time.

- How the system can handle the oversalling problem?
  here the role of consistency comes , so the last updated
  version of the system shall be obvious to the customer immediately

- How the system handle two orders can never claim the same last unit?
  here we can use a queue which can enhance the process , so we can see
  who the first one who ordered the last item and then we can assign it
  to it so no one else can order it.

- How the system handling that the customer order to be requested once?
  the point here is handled by cache abd the timestamp the cache will have
  the last order have been done by the customer and will be marked with the
  customer & order id . so if it is the same order from the same customer in
  time <300ms. then it shall be ordered once.