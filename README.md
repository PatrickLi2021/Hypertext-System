# Hypertext System

## Code:
Available upon request (patrick_li@brown.edu or patrickli2021@gmail.com)

## Introduction and Motivation:
A **_hypertext or hypermedia system_** platform that allows you to link an  access information of various kinds (i.e. text, images, video, etc.) as a web of nodes in which the user can browse at will. Hypertext documents are interconnected by hyperlinks that are typically activated by a mouse click, keypress set, or screen touch. The most famous implementation of hypertext is the World Wide Web, written in the final months of 1990 and released on the Internet in 1991. This project builds off of a common node file system - a standard way of managing and navigating between hypertext nodes. 

Examples of different types of text editors, all with very different features and use cases include:
- Google Docs (page breaks, basic tables, font color)
- Notion (code snippets, headings, quotes)
- Facebook (mentions, hashtags, photos)
- VSCode (automatically colors text based on language)

## Project Overview:
This project contains 3 parts: **database**, **backend**, and **frontend**. The backend is deployed on Google Firebase and the frontend via Heroku.

### Backend:

One of the files in the backend is `BackendNodeGateway.ts`, which is responsible for implementing the following methods:
- _createNode_: One of the core functionalities for this project is the ability to create nodes. This method creates a node in the MongoDB database.
- _getNodeById_: This function allows us to retrieve a node given the ID.
- _deleteAll_: This method deletes all documents in the MongoDB `nodes` collection. This method isn't needed much for production but rather for testing.
- _deleteNode_: This method allows users to delete a node and its children from the database given a `nodeId`.
- _moveNode_: This function takes in 2 `nodeId`'s, `nodeToMove`'s `nodeId` and `newParent`'s `nodeId`. The function also verifies if the move is valid and moves the node such that `nodeToMove` becomes a child of `newParent.`
- _addChild_: This method takes in a `childId` and `parentId` and update's a parent's `filePath.children` array with a new child `nodeId`. This is mainly used as a helper method for other functions.
- _removeChild_: This method takes in a `childId` and `parentId` and remove's `childId` from the parent's `filePath.children` array. This is mainly used as a helper method for other functions.

Another important file provided in the backend is `NodeCollectionConnection.ts`, which is used to help implement database queries in `BackendNodeGateway.ts`. Additionally, `server/src/types` includes important information on how the schema for `INode`'s, `IServiceResponse`'s, and other important data structures are created. The files in this folder also include type-checking functions such as `isNode()`.

## Frontend:
The frontend is built primarily in React and the primary file is `Nodeview.tsx`, which renders a node's data in a user-friendly UI. For the NodeView, the `title` of the node is clearly displayed, along with the `content` of the node and a breadcrumb. Additionally, there is a delete button that deletes the node when clicked.

Other important parts of the frontend include `FrontendNodeGateway`, `FrontendLinkGateway`, and `FrontendAnchorGateway`. Each of these gateways connects to a node backend, link backend, and anchor backend which each contain an Express router, backend gateway, and a CollectionConnection that connects directly to a MongoDB collection for nodes, links, and anchors.

For this project, `TextContent.tsx` is used to create the full texteditor while `TextMenu.tsx` is used for the text editor menu.

## Key Features:
- Editable hypertext nodes
- Resizable image nodes:
- CRUD operations on nodes
- Anchor and link creation and visual displays
