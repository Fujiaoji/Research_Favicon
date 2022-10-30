# The Security of ML
The whole framework
## 1. Different Class of attacks on ML systems (3 dimension for attacks tagainst learning system)
- Causative or Ecploratory
- Integrity or Availbility
- Targeted or Indiscriminate
## 2. Defends against attacks


# ML
## Notation
- False Positive: actual is 0, predict is 1
## 2. Framework
### 2.1 Security analysis
Properly analyze the security of a system requires identifying security goals and a threat model. 
- Definitions: 
  - Security: is concerned with protecting assets from attackers. 
  - Security goal: is a requirement that, if violated, results in the partial or total compromise of an asset. 
  - Threat model: is a profile of attackers, describing motivation and capabilities
#### 2.1.1 Security goals
In a security context, the classifier’s purpose is to classify malicious events and prevent them from interfering with system operations. Splitting the learning goal into two goals

下面的前提：the positive class (label 1) indicates malicious intrusion instances while the negative class (label 0) indicates benign normal instances. A classification error is a false positive (FP) if a normal instance is classified as positive and a false negative (FN) if an intrusion instance is classified as negative.

- Integrity goal: To prevent attackers from reaching system assets. False negatives violate the integrity goal: malicious instances that pass through the classifier can wreak havoc
- Availability goal: To prevent attackers from interfering with normal operation. False positives tend to violate the availability goal because the learner itself denies benign instances.
#### 2.1.2 Threat Model
 Some Definitions:
 - Attacker goal: the attacker wants to access system assets (typically with false negatives) or deny normal operation (usually with false positives)
### 2.2 Taxonomy: categorizing attacks against learning systems
- 1. Influence (the capacity of the attacker)
    - Causative attacks influence learning with control over training data: the attacker has the ability to influence the training data that is used to construct the classifier 
    - Exploratory attacks exploit misclassifications but do not affect training: the attacker does not influence the learned classifier, but can send new instances to the classifier and possibly observe its decisions on these carefully crafted instances
- 2. Security violation
    - Integrity attacks compromise assets via false negatives.
    - Availability attacks cause denial of service, usually via false positives.
- 3. Specificity
    - Targeted attacks focus on a particular instance: the attack is highly Targeted to degrade the classifier’s performance on one particular instance
    - Indiscriminate attacks encompass a wide class of instances.

### 2.3 Example
1与2的不同之处在于加了坏的之后被认为是好的还是坏的
- 1. Causative Integrity attack: the spam foretold. 例子：attacker send non-intrusion traffic that carefully chosen to resemble desired spam, to mis-train defender.
- 2. Causative Availability attack: the rogue filter. 例子：拦截合法的邮件，训练时，攻击者将spam与benign words联系起来，然后被定义为spam，在这些数据上训练时就会把好的分成坏的
- 3. Exploratary Intergrity attack: the shifty spammer. attacker crafts spam to evade classifier without influencing classifier directly. attacker modify spam and prevent denfender recognize the spam.
- 4. Exploratary Available attack: the mistaken identify, interfere with legistimate operation without influence over training. send many emails to the receiver and the user cannot find a good one
### 2.4 The Adversarial Game
exploratory Attack: att chooses a precedure for selecting evaluation distribution that affects evaluation data

Causative attack: choose precedure for selecting training distribution to manipulate training data

defender: choose learning algorithm

## 3. Attacks
## 4. Defender
### 4.1 defending against exploratory attacks
the attacker attempts to construct an unfavorable evaluation distribution concentrating probability mass on high- cost instances
#### 4.1.1 Defenses against attacks without probing
- Training data: Preventing the attacker from knowing the training data limits the attacker’s ability to reconstruct internal states of the classifier.
- Feature selection: it is a processs of choosing feature map that tranforms raw measurement into the feature space
- Hypothesis space/learning procedure: complex hypothesis space make it difficult for the attacker to infer info about the learned hypothesis

#### 4.1.2 Defenses against probing attacks
The ability for AE(procedure for selecting distribution) to query a classifier
- reverse engineering:  use queries to reverse engineer a classifier from a particular hypothesis class using a particular feature space. So just increase reverse difficulty
- Randomization: from {0, 1} to [0, 1]
- Limiting/misleading feedback

### 4.2 defending against Causative attacks
- Robustness: limit the impact of small fraction of deviant training data. It assumes that most data from known model, a fraction of data from ad
- Online Prediction with experts: dynamically adapt to the data in an online fashion.例子：a set of classifier, each designed to provide different security properties. the experts provide advice to the defender and produce a composite prediction. rather than evaluating the cost of the composite classifier’s predictions directly, we instead compare the cost incurred by the composite classifier rela- tive to the cost of the best expert in hindsight