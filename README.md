# hooksdemo
hooksdemo
 "Our security team is asking for help ensuring proper reviews are being done to code being added into our repositories. We have hundreds of repositories in our organization. What is the best way we can achieve at scale? We are new to some of the out-of-the-box settings and the GitHub API. Can you please help us create a solution that will accomplish this for our security team?"
-> /



# Create an organization
Go to Github -> create a new organization -> follow the steps


# Create an access token for the demo
Settings -> Developer settings -> Fine grained tokens -> generate new token
Give it a name
Set expiration
Change resource owner the be an organization 
Check repository and organizational perimissions (webhooks enable)
Generate!
Copy the output so you can use it as bearer in CLI code


# Create a webhook in CLI
-X POST \
-H "Accept: application/vnd.github+json" \
-H "Authorization: Bearer <YOUR-TOKEN>" \
https://api.github.com/orgs/ORG/hooks \
-d '{"name":"web","active":true,"events":["push","pull_request"],"config":{"url":"http://example.com/webhook","content_type":"json"}}'
  
  
ORG = organization name
<Your_token> = access token (keep secret)


# Create a listener on your localhost
require 'sinatra'
require 'json'
post '/payload' do
  push = JSON.parse(request.body.read)
  puts "I got some JSON: #{push.inspect}"
end


 
# Read more 
  How to create a webhook step by step - https://docs.github.com/en/rest/orgs/webhooks#create-an-organization-webhook
Best practices for integrators - https://docs.github.com/en/rest/guides/best-practices-for-integrators
Types of Github events - https://docs.github.com/en/developers/webhooks-and-events/events/github-event-types
  
