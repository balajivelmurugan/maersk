# maersk

**Task 1: Delete vendor**
		•	Approach: I implemented a delete operation for each row, ensuring users can remove items easily. To prevent accidental deletions, I added a confirmation popup so the user must explicitly confirm before the action is performed.
	•	Assumptions/Trade-offs: I assumed that deleting data should always require user confirmation, even if it adds one extra click, because data safety is more important than speed in this context.
	•	Challenges: The main challenge was ensuring the state/UI updated seamlessly after deletion. I addressed this by re-rendering the list immediately after the delete action and confirming the backend update.

 **Task 2: Fix the UI bug**
 	•	Approach: Initially, the form reset was delayed using a 2-second setTimeout, which unintentionally allowed users to click the submit button multiple times, leading to duplicate records in the database. I improved this by resetting the form immediately after receiving a success response from the server.
	•	Assumptions/Trade-offs: I assumed that preventing duplicate submissions is more critical than keeping the form open for convenience. This trade-off ensures data integrity and a smoother user experience.
	•	Challenges: The key challenge was identifying the cause of duplicate entries. Once I traced it to the delayed reset logic, the solution became clear—resetting immediately on success and ensuring the button state reflects the submission process.

 **Task 3: Unique Emails**
 	•	Approach: I implemented email uniqueness validation by checking directly against the database. When a user enters an email, the system queries the DB to see if it already exists. If it does, an error message is shown on the UI; otherwise, the user can proceed with registration.
	•	Assumptions/Trade-offs: I assumed that validating against the database is more reliable than relying only on frontend checks, as it ensures true uniqueness even if multiple users are registering simultaneously. The trade-off is a slight increase in server calls, but it guarantees data accuracy.
	•	Challenges: One challenge was deciding when to trigger the validation (on blur vs. on form submission). I chose validation during submission to avoid excessive DB calls while still ensuring the integrity of the data.

**1. What do I love most about being a software engineer?**
I love the ability to solve real-world problems through technology. Turning ideas into working solutions that positively impact users is extremely rewarding. I also enjoy the continuous learning that comes with this field there’s always a new challenge, framework, or concept to explore, which keeps me motivated and growing.

**2. What is most important to me when it comes to working in a team?**
Collaboration and open communication are most important. I value a team where ideas are freely shared, feedback is constructive, and everyone feels ownership of the work. I believe in helping teammates when they are stuck and also in learning from others. A supportive and transparent team environment not only builds better software but also makes the journey more enjoyable.

**3. What is the worst part of being a software engineer?**
The most challenging part can be dealing with unexpected bugs or changing requirements under tight deadlines. However, I see these situations as opportunities to improve problem-solving, adaptability, and resilience. While they can be stressful in the moment, overcoming them often leads to personal growth and stronger systems.

