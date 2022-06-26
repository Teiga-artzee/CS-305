# CS-305
Java Software Security Course Work and Projects
Alexandrea Teigeler
6/25/2022

#--------------------------------------------------------------------------------------------------------------#

Briefly summarize your client, Artemis Financial, and their software requirements 

#--------------------------------------------------------------------------------------------------------------#

1. Who was the client: 

Artemis Financial, who gives consultations for their customers regarding financial
planning, such as retirement funds, savings accounts, where to invest their captital, and insurance policies.

#--------------------------------------------------------------------------------------------------------------#

2. What issue did they want you to address: 

Artemis Financial needs to keep their clients private information safe, protect their employees personal identifying data, keep their websites application architeture hidden, and database
from being corrupted and compromised.

#--------------------------------------------------------------------------------------------------------------#

3. Identify their software security vulnerabilities: 

Website applications in particular must develop their security in such a way that can anticipate: 

+ SQL Injections -> When untrusted data is added to database queries, changing the structure of the application, and producing unanticipated behaviors; 

+ Broken Authentication -> To prevent this, have user sessions timeout, whitelist accepted characters known to be safe for passwords to prevent SQL Injection attakcs, and use Multifactor Authetication to increase the layers of security; 

+ IDOR -> Sanitize error messages to prevent exploitation of the websites URL; 

+ Input Verification -> verify that returned values are within the legal range, type data safely. Paramaterize every variable; 

+ API Interactions -> Spring Framework must support these interactions; 

+ Code Quality -> Use industry standards for application develop and best security practices.

#--------------------------------------------------------------------------------------------------------------#

4. Why is it important to code securely: 

If any of these vulnerabilities were exploited, there could be a loss of capital from the company and the clients, but Artemis Financials good reputation in the public eye would be lost and difficult to recooperate.

#--------------------------------------------------------------------------------------------------------------#

5. What value does software security add to a company’s overall wellbeing: 

Software Security protects their assets, such as their finanical capitial, keeps their industry secrets secure which prevents competiters from insight knowledge to their operations, protects their clients private information which provides trust between the company and the client.

#--------------------------------------------------------------------------------------------------------------#

6. What about the process of working through the vulnerability assessment did you find challenging or helpful:

The most challenging aspect was developing a RESTful API, as it was something I had never done before, as well as creating a server and connecting the application to that server, or supressing false positivies. I was unsucessful in parts of this endeavor, and have since continued to practice on these weak point in my skill set, 
as it is a vital part of my education and career as a computer scientist to be able to understand and put these concepts into practice. 

I feel that areas of help were the provided tutorials for setting up Maven Dependencies in the pom file.


#--------------------------------------------------------------------------------------------------------------#

7. How did you approach the need to increase layers of security? What techniques/strategies would you use in the future to assess vulnerabilities to determine mitigation techniques:

There were several applications that were sent over for review. I will detail my process for the "rest-service" application (Application can be found in this REPO). 

Upon receiving the "rest-service" application, I first ran a Maven Dependancy check to understand what are the known vulnerabilities within the libraries this application used. Uncovering the known vulnerabilities, and determining which ones were false positives, along with ones that did not apply to this current application ( due to being unutilized), allowed me to begin a manual review of the code to determine which portions of code were vulnerable to these known issues. There were four .java files that required refracturing, either due to the Dependancy Report, or poor coding quality standards:

1. DocData.java: This .java file had two main vulnerabilities that were uncovered:

+ Due to (CWE-209), printStackTrace has been known to generate a message which exposes information about the environment it runs in, users, and data.

+ Due to (CVE-2022-021724) & & (CVE-2020-13692) & (CVE-2021-44228), Connection con = DriverManager.getConnection(“jdbc:mysql://localhost:3306/test”, “root”, “root”) can cause JDBC vulnerability utilization URL attacks. The driver does not validate the class implementations for the expected interface. This leads to SQL injection attacks, man-in-the-middle attacker masquerading as a trusted user, improper authorization, XXE, access control bypass, priviledge escalation, arbitrary code execution, improper access control.

2. CrudController.java: This .java file had two main vulnerabilities that were uncovered:

+ Spring MVC automatic binding requiest parameters, it is possible to feed unexpected fields on arguments,	@RequestMapping(“/read”). This could provide unauthorized remote code execution if user input is used to change the content within the database.


+ toString(), the input values were never verified before the string is converted. SQL Injection is possible.

3. GreetingController.java: This .java file had three main vulnerabilities that were uncovered:

+ The variable 'name' is not checked for the correct type of input. SQL injection is possible.

+ .format, continuing from the previous issue, since it could possibily receive the wrong input, it could allow for an information leak and disclosure.

+ %s, could cause denial of service if the attacker injected characters into the string.


4. Greeting.java: This .java file had one main vulnerability that was uncovered:

+ GreetingController.java sends an atomic Long to Greeting.java, but the function Greeting only accepts Long. Sending different types of data can cause an interger underflow, which could leak data into other parts of the memory, causing data corruption.

After the vulnerabilities had been identified, a mitigation plan was developed that would be used to outline and guide the proper corrections:

1. It is important to handle exceptions internally. Do not display error messages containing sensitive information to the user.

2. Limit the amoint of JNDI data source names to the java protocol, as well as upgrading the packages to their latest versions to fix the known vulnerabilities.

3. Validate input of any untrusted data.

4. Ensure that as data transfers, data types match correctly.

#--------------------------------------------------------------------------------------------------------------#

9. How did you ensure the code and software application were functional and secure? After refactoring code, how did you check to see whether you introduced new vulnerabilities:

Running the Maven Dependency Check again after all false positives and unutilized library warnings were surpressed, illistrated first that the correct dependencies had been surpressed. Secondly, both Dependency Checks were examined to ensure that the list didn't illistrate that new vulnerabilites are risks were introduced, proving that the application was secure. Running the application, it was determined that if it run without error and performed as intended, it was fucntional.

#--------------------------------------------------------------------------------------------------------------#

10. What resources, tools, or coding practices did you employ?  Which ressources, tools, and coding practices would you find helpful in future assignments or tasks:

1. Apache Maven: Dependency Check tool
2. Developing secure code structure following Industry Standards.
3. Eclipse: IDE
4. Security Best Practices.

Understanding the inherit risks and vulnerabilities associated with web applications, preventing known attacks when writing secure code is essential. Writing code that can prevent these attacks by design, ensures that vulnerabilities are limited and greatly reduced before Security testing is performed.

#--------------------------------------------------------------------------------------------------------------#

11.Employers sometimes ask for examples of work that you have successfully completed to demonstrate:

+ Your skills

+ Knowledge

+ Experience. 

What from this particular assignment might you want to showcase to a future employer:

Skill Set: 
 
+ Manual Code inspection ->  To take knowledge about vulnerabilities from the Maven Dependency Check and insecure coding practices, and re-design the code and application in a way that prevents attackers from taking advanatage of these common weaknesses that web applications have. If updating the libraries are not an option, replacing insecure code with safe alternatives is ideal over using insecure code and adding additional structures to the code in order to avoid the vulnerability attack, which can bloat the overall application and run time. 

+ Maven Dependancy Check -> To edit the pom file of a Maven project. To run a clean install Maven configuration. Running a Maven Dependency Check. To create a surpression file for all codes that need to be surpressed. Updating the correlating libraries that have vulnerabilities associated with them.

Applicable Knowledge:

+ Manual Code inspection -> Able to sight read application code. To understand and recognize inherit risks from certain code design and practices. 

+ Maven Dependancy Check -> To read the dependency check. Determine which codes are serious vulnerabilities relating to the current application and which libraries would be affected by these codes. Determine which codes are false positives and those that should be surpressed. To know which libraries need to be updated.

Learned Experience: 

+ Secure Coding Practices

+ DevSecOps

+ Taking an issue presented by a client, understanding their industry and how best to suit their needs, applying knowledge of what might be a security concern and drafting up a vulnerability assessment that underscores the importance of each step taken to make their software secure for them and their customers.
