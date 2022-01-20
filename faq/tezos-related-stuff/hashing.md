# Hashing

### It seems amazing that it's possible to hash this huge, seemingly infinite space of byte sequences without collisions. An intuition as to why this works?

**Answer** (direct quote from Corneliu Hoffman) Well hashing will eventually collide of course. The point is that you do not hash the entire universe at the same time. Here is a very simple model. Suppose your hashing function just picks a random element from 0-9 and you want to has the universe. What are the chances that the two elements you choose to hash are different (do nor collide)? 90%. For three is 72% and for 4 it is a bit over 50. So remarkably enough, a random one digit hash is more likely than not to be enough to hash 4 objects. You can make things precise using Stirling's approximation of factorial.
