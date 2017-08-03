Guidelines for Service Token use:
----------------------------------
1) Use one token for one purpose only (for example, one token for all travis apps)
2) Maintain a list of places where the token is used. In case you need to revoke the token, this list will be helpful to quickly make the necessary token updates prior to revoking the token.
3) Always generate new encryption key for each use
4) Determine and be aware of scope of vulnerability of the token
5) Never store unencrypted secret on the network
6) Revoke if you have any fear that secret has been compromised
