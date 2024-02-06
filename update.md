---
permalink: /update
---

<html>
<div>
<pre id = "data"></pre>
<form>
<input type="text" id = "username" class = "input" placeholder = "new username">
<br>
<input type="text" id = "uid" class = "input" placeholder = "old username">
</form>
<br>
<button class = "submit" onclick = "update()">Change</button>
</div>
</html>
<script>
function update() {
    data = {
        "name": document.getElementById("username").value,
        "uid": document.getElementById("uid").value,
        "role": "admin"
    }
    let options = {
    method: 'PUT',
    headers: {
        'Content-Type': 'application/json;charset=utf-8',
    },
    credentials: 'include',
    body: JSON.stringify(data)
}
    fetch("http://127.0.0.1:8086/api/users/", options)
        .then(response => {
            let access = response.status !== 401 && response.status !== 403;
            return response.json().then(data => ({ data, access }));
        })
        .then(({data, access}) => {
            console.log(access)
            if (access){ 
            document.getElementById("data").textContent = "Data Successfully Changed";
            }
            else {
                document.getElementById("data").textContent = "Unauthorized.";
            }
        })
}
</script>