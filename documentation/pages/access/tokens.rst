.. _tokens:

Tokens
^^^^^^

Repository tokens are used by the client APIs.  Optionally, a repository could be set up to allow API access without
a token (Repository > Settings > Configuration > API Settings), by default,  token is required for both API push and
pull.



.. image:: /images/token.png


1. Token name has to be unique among tokens.
2. Expiration date is optional.  If set, token will no longer be accepted after the expiration is reached.
3. Push Key Override - if enabled will allow property value Push via API, regardless of the property key's Push setting.
4. Push Access Rules - let's you specify a team.  Access rules defined for the team will be applied for all API Push requests issued by the client.
5. Security Groups entered into this field will pre-authorize the token to decrypt values and files assigned to them prior to returning the data via API Pull request.
6. Managed By - let's you specify who has visibility to this token.