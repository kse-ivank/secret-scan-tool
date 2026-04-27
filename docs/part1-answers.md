## Part 1 – Questions to Answer

**1. Why do some rules have an entropy threshold and others don't?**  
Some secret patterns look similar to harmless strings, so the rules for them add an entropy threshold to only keep matches that are sufficiently random, which reduces false positives. Other patterns are already distinctive enough that entropy doesn't add much value, so those rules omit the threshold to keep the logic simpler and avoid accidentally dropping valid matches

**2. What is the purpose of secret_group and which rules use it?**  
secret_group tells the scanner which regex capture group actually contains the sensitive value to run entropy checks, instead of using the entire match. It's used in rules where the full pattern includes non secret context and only a portion of the match is the secret itself, so that the scanner evaluates and prints just that portion rather than the whole string

**3. How does the keyword pre-filter improve performance?**  
The keyword pre-filter quickly checks each line for a small set of cheap substring matches at the beginning. If none of keywords appear in the line, the regex for that rule is skipped entirely on that line, which  reduces the number of regex evaluations so it results with faster scanning
