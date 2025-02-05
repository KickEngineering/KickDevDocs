## Scopes

Scopes enable an app to request a level of access to Kick and define the specific actions applications can perform.

These scopes are for apps using OAuth 2.1 authorization code grants for authorization. The title is displayed to the user on the consent screen during the authorization flow.

<table>
   <thead>
      <tr>
         <th width="266">Scope</th>
         <th>Summary</th>
         <th>Description</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>
            <code>user:read</code>
         </td>
         <td><span data-gb-custom-inline data-tag="emoji" data-code="2705">Read user info</span></td>
         <td>View user information in Kick including username, StreamerID, etc.</td>
      </tr>
      <tr>
         <td>
            <code>channel:read</code>
         </td>
         <td><span data-gb-custom-inline data-tag="emoji" data-code="2705">Read channel info</span></td>
         <td><span data-gb-custom-inline data-tag="emoji" data-code="2705">View channel information in Kick including Channel description, category, etc</span></td>
         <td></td>
      </tr>
      <tr>
         <td>
            <code>channel:write</code>
         </td>
         <td><span data-gb-custom-inline data-tag="emoji" data-code="2705">Update Channel info</span></td>
         <td>Update livestream metadata for a channel based on the channel ID.</td>
      </tr>
      <tr>
         <td>
            <code>streamkey:read</code>
         </td>
         <td><span data-gb-custom-inline data-tag="emoji" data-code="2705">Read streamkey</span></td>
         <td>Read a user's StreamURL and Stream key</td>
      </tr>
       <tr>
         <td>
            <code>events:subscribe</code>
         </td>
         <td><span data-gb-custom-inline data-tag="emoji" data-code="2705">Subscribe to events</span></td>
         <td>Subscribe to all channel events like chat messages, follows, subscribe and gifts on Kick</td>
      </tr>
    </tbody>

 
   
</table>