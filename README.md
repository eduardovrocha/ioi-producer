# Music Producer Application Documentation

### Briefing Transcription:
Aplicação concebida para atender às necessidades de um produtor musical que oferece serviços 
personalizados para diversos clientes. O objetivo é fornecer uma plataforma robusta e intuitiva 
que permita ao produtor e seus clientes gerenciarem o processo de criação, revisão e entrega 
de áudios de maneira eficiente.

O produtor musical contará com um painel web que possibilita o envio de arquivos de áudio e a
inclusão de comentários em cada versão enviada. Esse painel oferece flexibilidade, permitindo 
que o produtor envie quantos áudios forem necessários até que o cliente esteja satisfeito com
o resultado final. Ao concluir o processo, o produtor poderá compactar os arquivos aprovados
em um único pacote no formato zip e disponibilizá-lo para download através da plataforma.

Por sua vez, o cliente terá acesso a um aplicativo móvel que permite a audição das versões de
áudios enviadas pelo produtor, a inclusão de comentários específicos para cada arquivo e a 
aprovação das versões finais. Após a aprovação, o cliente poderá realizar o pagamento por 
meio do sistema PayPal, garantindo uma transação segura e ágil. Após a confirmação do pagamento, 
o cliente receberá automaticamente um link para download do conteúdo final aprovado e compactado, 
facilitando a entrega e o acesso ao material produzido.

## Table of Contents
1. [API Backend Documentation](#api-backend-documentation)
2. [Producer Panel Views](#producer-panel-views)
3. [Mobile App Views (Client)](#mobile-app-views-client)

---

## API Backend Documentation

### Overview
This API serves as the backend for a music production management system. It provides endpoints for both the music producer and the clients to manage, upload, comment on, approve, and download audio files, as well as handle payments via PayPal.

#### Base URL
```
https://api.musicproducerapp.com/v1
```

### Endpoints

#### Authentication
1. **POST /auth/login**
    - **Description:** Authenticate user (Producer or Client).
    - **Payload:**
      ```json
      {
        "email": "string",
        "password": "string"
      }
      ```
    - **Response:**
      ```json
      {
        "token": "string"
      }
      ```

2. **POST /auth/register**
    - **Description:** Register a new client.
    - **Payload:**
      ```json
      {
        "name": "string",
        "email": "string",
        "password": "string"
      }
      ```
    - **Response:**
      ```json
      {
        "message": "string"
      }
      ```

#### Audio Management
3. **POST /audios**
    - **Description:** Upload a new audio file by the producer.
    - **Payload:**
        - Multipart/form-data with `file` and optional `comments`.
    - **Response:**
      ```json
      {
        "audio_id": "integer",
        "message": "string"
      }
      ```

4. **GET /audios**
    - **Description:** List all audio files for a project.
    - **Query Parameters:**
        - `project_id`: integer
    - **Response:**
      ```json
      [
        {
          "audio_id": "integer",
          "file_url": "string",
          "comments": "string",
          "status": "string"
        }
      ]
      ```

5. **PUT /audios/:id/comments**
    - **Description:** Add comments to an audio file.
    - **Payload:**
      ```json
      {
        "comments": "string"
      }
      ```
    - **Response:**
      ```json
      {
        "message": "string"
      }
      ```

6. **PUT /audios/:id/approve**
    - **Description:** Approve an audio file by the client.
    - **Response:**
      ```json
      {
        "message": "string"
      }
      ```

#### Payment
7. **POST /payments**
    - **Description:** Process a payment via PayPal.
    - **Payload:**
      ```json
      {
        "audio_id": "integer",
        "amount": "float"
      }
      ```
    - **Response:**
      ```json
      {
        "payment_status": "string",
        "download_link": "string"
      }
      ```

---

## Producer Panel Views
1. **Dashboard**
    - Overview of ongoing and completed projects.
    - Quick actions: Upload new audio, view client comments.

2. **Project Management**
    - List of all projects with status and client details.
    - Option to create new projects.

3. **Audio Upload**
    - Form to upload new audio files with comments.

4. **Comments & Feedback**
    - View comments from the client for each audio file.
    - Add producer comments.

5. **Finalize & Zip Files**
    - Create and upload a zipped file for the approved project.

6. **Account Settings**
    - Update profile and manage account details.

---

## Mobile App Views (Client)
1. **Login & Registration**
    - Secure authentication.

2. **Dashboard**
    - Overview of projects and their statuses.

3. **Project Details**
    - List of audio files for a project.
    - Play audio files.
    - Add comments.

4. **Audio Approval**
    - Button to approve audio after review.

5. **Payment Screen**
    - Interface to handle PayPal payments.

6. **Download Section**
    - Download link for the approved, zipped project.

7. **Profile Settings**
    - Manage account details.
