<script>
  let users = [
    {
      id: 0,
      name: 'Abdul Basit',
      age: 26,
      country: 'Pakistan',
    },
    {
      id: 1,
      name: 'Ahmed',
      age: 24,
      country: 'Pakistan',
    },
  ]
  let data = {
    name: '',
    age: '',
    country: '',
    id: null,
  }
  let addUser = () => {
    const newUser = {
      id: Date.now() + Math.random(),
      name: data.name,
      age: data.age,
      country: data.country,
    }
    users = users.concat(newUser)
    data = {
      name: '',
      age: '',
      country: '',
      id: null,
    }
    console.log(users)
  }
  let isEdit = false
  let editUser = (user) => {
    isEdit = true
    data = user
  }
  let updateUser = () => {
    isEdit = !isEdit
    let userDB = {
      name: data.name,
      age: data.age,
      country: data.country,
      id: data.id,
    }
    let objIndex = users.findIndex((obj) => obj.id == userDB.id)
    users[objIndex] = userDB
    data = {
      id: null,
      name: '',
      age: '',
      country: '',
    }
  }
  let deleteUser = (id) => {
    console.log(id)
    users = users.filter((user) => user.id !== id)
  }
</script>

<section>
  <h1>Svelte Basic CRUD APP</h1>
  <h5>Add New User</h5>
  <form>
    <div>
      <label for="name">Name</label>
      <input
        bind:value={data.name}
        type="text"
        id="text"
        placeholder="Enter Name"
      />
    </div>
    <div>
      <label for="age">Age</label>
      <input
        bind:value={data.age}
        type="number"
        id="text"
        placeholder="Enter Age"
      />
    </div>
    <div>
      <label for="country">Country</label>
      <input
        bind:value={data.country}
        type="text"
        id="text"
        placeholder="Enter Country"
      />
    </div>
    {#if isEdit === false}
      <button type="submit" on:click|preventDefault={addUser}>
        Add User
      </button>
    {:else}
      <button type="submit" on:click|preventDefault={updateUser}>
        Edit User
      </button>
    {/if}
  </form>

  <div style="overflow-x:auto;">
    <h5>User details</h5>
    <table>
      <tr>
        <th> Name </th>
        <th> Age </th>
        <th> Country </th>
        <th> Action </th>
      </tr>
      {#each users as user}
        <tr>
          <td>
            {user.name}
          </td>
          <td>
            {user.age}
          </td>
          <td>
            {user.country}
          </td>
          <td>
            <button on:click={editUser(user)}>Edit</button>
            <button on:click={deleteUser(user.id)}>Delete</button>
          </td>
        </tr>
      {/each}
    </table>
    <!-- {user.name} is {user.age} years old and lives in {user.country} -->
  </div>
</section>

<style>
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 300;
    text-align: center;
  }
  h5 {
    font-weight: bold;
    text-transform: uppercase;
    color: #ff3e00;
  }

  table {
    border-collapse: collapse;
    border-spacing: 0;
    width: 100%;
    border: 1px solid #ddd;
  }

  th,
  td {
    text-align: left;
    padding: 8px;
  }

  tr:nth-child(even) {
    background-color: #f2f2f2;
  }
</style>
