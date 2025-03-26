AHP (Analytical Hierarchical Process):
- Multi Criteria decision making method that was originally developed by Prof. Thomas L. Saaty
- It derives a ratio scales from paired comparisons of criteria and evaluation:
	- To make more comparisons we still make them in pair but make more comparisons:
		- ![[Pasted image 20250227103749.png]]
	- From that we can make matrices of comparison using the following rules:
		- The diagonal elements of the matrix are always 1
		- If the judgment value is on the left side of 1, we put the actual judgment value.
		- If the judgment value is on the right side of 1, we put the reciprocal value.
		- Fill the symmetric matrix with inverse values
		- Calculate the columns sum
		- Normalize the matrix dividing each element with the sum of its column: now each column sum is 1
		- The normalized eigenvector (Priorities Vector) is obtained by averaging across the rows
		- Example:
		- ![[Pasted image 20250227104129.png]]
		- ![[Pasted image 20250227104152.png]]
		- ![[Pasted image 20250227104204.png]]
		- ![[Pasted image 20250227104217.png]]
		- ![[Pasted image 20250227104231.png]]
	- 
Example:
- Estimating costs:

|      | Req1 | Req2  | Req3 | Req4 |
| ---- | ---- | ----- | ---- | ---- |
| Req1 | 1    | 1/3   | 2    | 4    |
| Req2 | 3    | 1     | 5    | 3    |
| Req3 | 1/2  | 1/5   | 1    | 1/3  |
| Req4 | 1/4  | 1/3   | 3    | 1    |
| SUM  | 19/4 | 28/15 | 11   | 25/3 |
- Normalize colomns:

|      | Req1  | Req2  | Req3 | Req4  |
| ---- | ----- | ----- | ---- | ----- |
| Req1 | 4/19  | 5/28  | 2/11 | 12/25 |
| Req2 | 12/19 | 15/28 | 5/11 | 9/25  |
| Req3 | 2/19  | 3/28  | 1/11 | 1/25  |
| Req4 | 1/19  | 5/28  | 3/11 | 3/25  |
| SUM  | 1     | 1     | 1    | 1     |
- Sum the rows and final result:

|      | Req1         | Req2         | Req3        | Req4         | SUM  | SUM/n |
| ---- | ------------ | ------------ | ----------- | ------------ | ---- | ----- |
| Req1 | 4/19 = 0.21  | 5/28 = 0.18  | 2/11 = 0.18 | 12/25 = 0.48 | 1.05 | 0.231 |
| Req2 | 12/19 = 0.63 | 15/28 = 0.54 | 5/11 = 0.45 | 9/25 = 0.36  | 1.98 | 0.524 |
| Req3 | 2/19 = 0.11  | 3/28 = 0.11  | 1/11 = 0.09 | 1/25 = 0.04  | 0.34 | 0.095 |
| Req4 | 1/19 = 0.05  | 5/28 = 0.18  | 3/11 = 0.27 | 3/25 = 0.12  | 0.62 | 0.15  |
| SUM  | 1            | 1            | 1           | 1            | 4    | 1     |

|           | SUM  | SUM / n | Result |
| --------- | ---- | ------- | ------ |
| Req1      | 1.05 | 0.231   | 23.1%  |
| Req2      | 1.98 | 0.524   | 52.4%  |
| Req3      | 0.34 | 0.095   | 9.5%   |
| Req4      | 0.62 | 0.15    | 15%    |
| SUM (= n) | 4    | 1       | 100%   |

Comunication, the rule of 5Cs of written com.:
- Correct grammar and spelling.
- Concise expression - elimination of excess words.
- Clear purpose.
- Coherent logical flow of ideas.
- Controlling the flow of the words and ideas- using graphics and needed.
Comunication grows with more and more people following the rule: n(n) ??
Project managers cannot control all comunication, trying to do so should keep ...
Processes of comunications:
- Listening:
	- Pretend.
	- Inattentive.
	- Misunderstood.
	- Biased.
		- Listening for facts and confirmations on personal biases and presumptions. 
	- Empathetic.
	- Engaged.
- Effective listening
- feedback
- Nonverbal
Communication methods:
- Formal meeting
- Informal meeting
- Conference call
- Web conference
- Video conference (as web conference but with webcam)
- Status report
- E-mail
- Phone call
- Voice mail
- Webinar
- Blog
- Social media
- Extra-net or shared folders
- Newsletter
- 

