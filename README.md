# ApplicationFormsAPI
**1. Application Overview:**

Purpose: The application allows employers to create application forms with various question types (Paragraph, YesNo, Dropdown, MultipleChoice, Date, Number) using CRUD (Create, Read, Update, Delete) operations.
Backend: Built with .NET 8, it utilizes ASP.NET Core for web API development.
Database: Uses Azure Cosmos DB, a NoSQL database, for storing application form questions (QuestionsContainer) and candidate submissions (CandidateContainer).

**2. Components:**

Models and DTOs: Defined based on designs from Figma, representing entities like questions (Question) and candidate submissions (CandidateSubmission).
Services: Implements business logic and interacts with Azure Cosmos DB using CosmosDbService, managing operations for questions and candidate submissions asynchronously.
Controllers: Includes QuestionsController and CandidateController to handle HTTP requests for CRUD operations on questions and submission handling respectively.

**3. Dependency Injection:**

Configured in Program.cs, it injects CosmosDbService with Cosmos Client to manage connections and operations on multiple containers (QuestionsContainer and CandidateContainer).
Endpoints:

**4. Questions API (/api/questions):**
Allows creating, reading, updating, and deleting questions. Supports different question types and retrieves questions based on type or all questions. Azure Cosmos DB has database created as QuestionsDB with container QuestionsContainer with partial key as /Type.
API URLs: <img width="296" alt="image" src="https://github.com/ashwinis29/ApplicationFormsAPI/assets/140146016/8643ff22-e81e-473e-994b-f9570e74fbde">
Example of Post API: 

Request: 
{
  "id": "",
  "type": "Dropdown",
  "text": "What is your preferred programming language?",
  "options": [
    "JavaScript", "Python", "C#"
  ],
  "enableOtherOption": true
}

Response: 
<img width="328" alt="image" src="https://github.com/ashwinis29/ApplicationFormsAPI/assets/140146016/6bf03aeb-e649-4268-80fb-d1e056356889">

Stored in Azure Cosmos DB: 
<img width="467" alt="image" src="https://github.com/ashwinis29/ApplicationFormsAPI/assets/140146016/c58c9ed6-f558-44d5-ab70-2bdcfdd904bd">



**5. Candidates API (/api/candidates):** 
Provides endpoints for candidates to submit responses (/submit) and for rendering questions (/questions) to the frontend based on their types. Azure Cosmos DB has database created as QuestionsDB with container CandidateContainer with partial key as /CandidateId.
API URLs: <img width="286" alt="image" src="https://github.com/ashwinis29/ApplicationFormsAPI/assets/140146016/adeec708-f513-4416-8990-efab9562f27a">

Example of Post API: 

Request: 
{
  "id": "",
  "candidateId": "",
  "candidateName": "Ashwini P S",
  "candidateQuestions": [
    {
      "questionType": "YesNo",
      "questionText": "Have you ever been rejected by UK embassy?",
      "answer": "No"
    }
  ]
}

Response: 
<img width="377" alt="image" src="https://github.com/ashwinis29/ApplicationFormsAPI/assets/140146016/55bcb5e7-c7b3-4b68-abee-394fb13e9f78">

Stored in Azure Cosmos DB: 
<img width="416" alt="image" src="https://github.com/ashwinis29/ApplicationFormsAPI/assets/140146016/992111c1-65f8-4dcf-968e-60b2147e478f">




**6. Integration and Testing:**

Utilizes Azure Cosmos DB Emulator for local development and testing.
Implements Swagger UI (/swagger) for API documentation and testing during development.
Includes NUnit for QuestiosController.cs and CandidateController.cs file.

**7. Deployment and Environment:**

Suitable for deployment to Azure App Service or other hosting platforms compatible with .NET applications.
Configures environments (IsDevelopment()) to enable Swagger UI and other debugging tools selectively.
