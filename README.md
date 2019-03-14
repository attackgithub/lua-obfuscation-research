# lua-obfuscation-research
All of _my_ code should be considered under the GNU Affero GPL v3. 


Code generated using my code should not be used as copy-protection, DRM, etc., or anything else to obscure reverse engineering. I did this for research. If someone uses this to obfuscate their code, and it is within legal bounds (i.e., you are a security researcher unfamiliar with Lua, and this was used maliciously) and you would like assistance reverse engineering code generated by this, feel free to ask me for help. Though I very highly doubt that you will need it. 


A stupidly large amount of code here belongs to other people, like mlnlover11, the creator of XFuscator, and Stravant, creator of an amazingly well written Lua formatter. I just wrote obfuscation passes on top of their code. 


The most notable novelty(?) here, in my opinion, is **constant comparison obfuscation**. A comparison to a constant is replaced by a (memoizable) comparison to a hash of said constant. For example: 


```lua
if x == 'Hello' then
  print ' world!'
end
```

Can be replaced by something like: 


```lua
if type(x) == 'string' and md5(x) == '8b1a9953c4611296a827abf8c47804d7' then 
  print ' world!'
end
```

The use of a quicker and/or more secure hash function, a salt, and/or multiple rounds of a hash function can be used to improve upon this concept. The potential is to completely and irreversibly eliminate some information (constants) from the codebase in special circumstances.
