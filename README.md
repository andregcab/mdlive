# mdlive


In the example below, I will demonstrate my understaning of pagination and how it applies to Ruby and the challenge given. 

Some things to note: 
  - I have no previous experience in Ruby
  - I made a conscious decison to present this in a github and only in the README
  
  
Pagination is essentially the method of dividing data into more useful pieces. Below is an example of my use of pagination using fetch in a React app. This example can be found in my own repository here => https://github.com/andregcab/reporting-interview-challenge-js-1/blob/master/src/fetch-users.js


const USER_API_ENDPOINT = "/api/users";

export const fetchUsers = () => {
  // Currently, this function only fetches a subset of all the users because the API only returns up to 50 users at a time
  // The API supports two pagination parameters: `limit` and `offset`
  // You can see the API response using this URL in your browser: http://localhost:3001/api/users?pretty=true
  // The CHALLENGE is to update this function to return a promise with the list of all users and the total number of users,
  // in the format:
  // { items: [], _total: 0 }
  // You can read README.md for more info
  return new Promise((resolve, reject) => {
    let users = [];
    getUsers(USER_API_ENDPOINT, users, resolve, reject);
  })  

};

const getUsers = (url, users, resolve, reject) => {
  fetch(url)
    .then((results) => {
    return results.json()
    })
    .then(results => {
      users.push(...results.items);
      // console.log(users);
      if (results._links.next.href !== null) {
        // console.log(results._links.next.href)
        getUsers(results._links.next.href, users, resolve, reject);
      } else {
        resolve({items: users, _total: results._total})
      }
    })
    .catch(error => {
    reject(error);
  })
}


.
.
.
.
.
.

In the case of this challenge using Ruby, it is my understanding that kaminari is a part of the default Gemfile. The controller is below

def index
   @apps = Apps.order(:name).page params[:page]
  
  
  "# GET /apps/1"
  "# GET /apps/1.json"
  
  def show
  end
  
  
  *the view file will show.... <%= paginate @apps, params: { "range": { "by": "name", "start": "my-app-001", "end": "my-app-050", "max": 10, "order": "asc" } } %>


.
.
.
.

I had a bit of trouble finding ways to pagniate with Ruby other than using gems and Kaminari seemed to be the most used one, again I hope this is not outside of the requirements. I expect my solution is not exact, however my goal was to demonstrate a basic understanding. With a little bit of teaching I am certain I uderstand Ruby in a very short amount of time given the time it took me to grasp JavaScript. Thank you for your time in reviewing my submission. 
