<script>
  let posts = [
    {
      id: 1,
      name: "Como instalar svelte",
      description: "lorem	ipsum lorem ipsum lorem ipsum",
      category: "Svelte",
      imageUrl: "https://srojas.dev"
    },
    {
      id: 2,
      name: "Svelt sin virtual DOM",
      description: "lorem	ipsum lorem ipsum lorem ipsum",
      category: "Svelte"
    }
  ];

  let post = {
    id: "",
    name: "",
    description: "",
    category: ""
  };

  let editStatus = false;

  const clearPost = () => {
    post = {
      id: "",
      name: "",
      description: "",
      category: ""
    };
  };

  const addPost = () => {
    const newPost = {
      id: posts.length + 1,
      name: post.name,
      description: post.description,
      category: post.category
    };
    posts = posts.concat(newPost);
    clearPost();
  };

  const updatePost = () => {
    let updatedPos = {
      id: post.id,
      name: post.name,
      description: post.description,
      category: post.category
    };

    const postIndex = posts.findIndex(p => p.id === post.id);
    posts[postIndex] = updatedPos;
    editStatus = false;
    clearPost();
  };

  const onSubmitHandler = e => {
    e.preventDefault();
    if (!editStatus) {
      addPost();
    } else {
      updatePost();
    }
  };

  const deletePost = id => {
    posts = posts.filter(post => post.id !== id);
  };

  const editPost = postEdited => {
    post = postEdited;
    editStatus = true;
  };
</script>

<style>
  main {
    max-width: 1200px;
    margin-left: auto;
    margin-right: auto;
    padding: 0 15px;
  }
  .logo-svelte {
    margin: 50px 0;
  }
  .cont-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 40px;
  }
  form {
    display: flex;
    width: 50%;
    flex-direction: column;
    padding: 20px;
    border-radius: 8px;
    background-color: #fa3e01;
  }
  input,
  select,
  textarea {
    font-family: "Poppins", sans-serif;
    font-size: 12px;
    font-weight: 300;
    color: #fff;
    padding: 8px 12px;
    margin-bottom: 10px;
    resize: none;
    border-radius: 4px;
    border: none;
    background-color: #ffffff47;
  }
  input:focus,
  select:focus,
  textarea:focus {
    outline: none;
  }
  ::placeholder {
    color: white;
  }
  .card {
    padding: 20px;
    margin-bottom: 40px;
    border-radius: 8px;
    box-shadow: 8px 14px 38px rgba(39, 44, 49, 0.06),
      1px 3px 8px rgba(39, 44, 49, 0.03);
  }
  strong {
    font-weight: 500;
    color: #ff3e00;
  }
  p {
    font-weight: lighter;
    margin: 0;
  }
  button {
    font-size: 12px;
    color: #fff;
    padding: 5px 10px;
    margin-top: 14px;
    margin-right: 8px;
    cursor: pointer;
    border: none;
    border-radius: 4px;
  }
  .button--delete {
    background-color: #ff3e00;
  }
  .button--edit {
    background-color: #1abc9c;
  }
  .button--form {
    font-weight: bold;
    color: #fa3e01;
    padding: 10px 0;
  }
</style>

<main>
  <img
    src="https://svelte.dev/svelte-logo-horizontal.svg"
    class="logo-svelte"
    width="18%"
    alt="" />
  <div class="cont-grid">
    <div class="cont-grid__child">
      {#each posts as item}
        <div class="card">
          <strong>{item.name}</strong>
          <p>{item.description}</p>
          <p>{item.category}</p>
          <button class="button--delete" on:click={deletePost(item.id)}>
            Delete
          </button>
          <button class="button--edit" on:click={editPost(item)}>Edit</button>
        </div>
      {/each}
    </div>
    <div class="cont-grid__child">
      <form on:submit={onSubmitHandler}>
        <input
          bind:value={post.name}
          type="text"
          id="post-name"
          placeholder="Post name" />
        <textarea
          bind:value={post.description}
          id="post-description"
          rows="3"
          placeholder="Post description" />
        <select bind:value={post.category} id="post-category">
          <option>Seleccionar</option>
          <option value="angular">Angular</option>
          <option value="svelte">Svelte</option>
          <option value="react">React</option>
          <option value="vue">Vue</option>
        </select>
        <button class="button--form">
          {#if !editStatus}Save Post{:else}Update Post{/if}
        </button>
      </form>
    </div>
  </div>

</main>
