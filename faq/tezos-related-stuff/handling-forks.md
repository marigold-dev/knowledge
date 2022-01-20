# Handling forks

### The doc says the old network surrenders to the new network and that both chains can live independently. How?

**Question:** The doc says that the entire old network must surrender to the new network but also that at the end we can have both the forked and the initial blockchain lives independently. How it can be possible if the entire old network has to update to the new forked one? How does it work in practice? As a user, can I be a node on both? In a proof of work context, I understand that we trust the longest chain, but if tomorrow a miner get 51% of the cpu power and manages to build the new longest chain, we will trust this by default. So how, as nodes, can we figured out that this longest chain is a fraud and what can we do about it?

**Answer** You could have checkpoint rules that refuse forks older than 2 weeks old or that 5 cycles ago. This is how Tezos addresses those issues.
