### Graph QL

#### query

query GET_AUTHORS {
  authors {
    name
    role
    description
  }
}

query GET_LANDING_PAGE {
  ladingPage {
    logo {
      alternativeText
      url
    }
  }
}

#### query com parametros

query GET_AUTHOR($id: ID!){
  author(id: $id) {
    id
    name
    role
    description
  }
}

#### query não nomeada

{
  author(id: 4) {
    id
    name
    role
    description
  }
}

#### fragments

fragment imageData on UploadFile {
   alternativeText
   url
}

fragment logo on LadingPage {
  logo {
      ...imageData
    }
}

fragment header on LadingPage {
  header {
      title
      description
      button {
        label
        url
      }
      image {
        ...imageData
      }
    }
}

query GET_LANDING_PAGE {
  ladingPage {
    ...logo
    ...header
  } 
}

#### query com alias

query GET_LANDING_PAGE {
  ladingPage {
    createdAt: created_at
    ...logo
    ...header
  } 
}

#### mutation update

mutation UPDATE_AUTHOR {
  updateAuthor(input: {where: { id: 4 }, data: {name: "Willian Justen"}}) {
    author {
    	id
      name
      role
  	}
  }
}

mutation UPDATE_AUTHOR($id: ID!, $data: editAuthorInput) {
  updateAuthor(input: {where: { id: $id }, data: $data}) {
    author {
    	id
      name
      role
  	}
  }
}

#### mutation create

mutation CREATE_AUTHOR {
  createAuthor(input: {data: {name: "Novo Instrutor", role: "instrutor", description: "Blabla"}}) {
    author {
      id
      name
      role
    }
  }
}


#### mutation delete

mutation DELETE_AUTHOR {
  deleteAuthor(input: {where: {id: 4}}) {
    author {
      id
      name
      role
    }
  }
}


