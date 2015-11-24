# Intuitionistic Propositional Logic

## Terms

- Premises & Conclusion

  Premise **implies** Conclusion, but

  Conclusion *does not* **imply** premises.

- Judgement

  Judgement is donoted by **Γ ⊢ P**, where

  P is a proposition, and Γ is a set of propositions

  > With the context Γ, we can infer that
P holds.

- Derivation

  Bottom-up approaches to decompose conclusions into a set of propositions.

  Notations:

  ```
  // J1 and J3 are axioms

             ----
              J3
  ----       ----
   J1         J2
  ---------------
        J
  ```

## Rules

- Hypothesis Rule

  if P ∈ Γ, we then have:

  ```
  --------- (hyp)
    Γ ⊢ P
  ```

  Example:

  ```
  --------------- (hyp)
    {P, Q} ⊢ P
  ```

  Given Γ = {P, Q, R}:

  ```
  ---------- (hyp)
    Γ ⊢ P
  ```

- Conjunction

  Formation Rule:

  ```
  // what the hack is this markdown formatter...
    A and B are propositions
  ----------------------------
    A ∧ B is a proposition
  ```

  Introduction Rule:

  ```
  // Seriously, no indention on the first line?
      Γ ⊢ A     Γ ⊢ B
  ----------------------- (∧-intro)
        Γ ⊢ A ∧ B
  ```

  Elimination Rules:

  ```
  // remove the right hand side element
      Γ ⊢ A ∧ B
  ----------------- (∧-elimL)
        Γ ⊢ A
  ```

  ```
  // remove the left hand side element
      Γ ⊢ A ∧ B
  ----------------- (∧-elimR)
        Γ ⊢ B
  ```

- Implication

  Formation Rule:
  ```
  //
    A and B are propositions
  ----------------------------
    A -> B is a proposition
  ```

  Introduction Rule:
  ```
  //
    Γ, A ⊢ B
  ------------- (-> - intro)
    Γ ⊢ A → B
  ```

  Elimination Rule:
  ```
  //
    Γ ⊢ A -> B      Γ ⊢ A
  -------------------------- (-> - elim)
            Γ ⊢ B
  ```

- Disjunction

  Formation Rule:
  ```
  //
    A and B are propositions
  ----------------------------
    A ∨ B is a proposition
  ```

  Introduction Rules:
  ```
  //
      Γ ⊢ A
  -------------- (∨-introL)
    Γ ⊢ A ∨ B
  ```

  ```
  //
      Γ ⊢ B
  ------------- (∨-introR)
    Γ ⊢ A ∨ B
  ```

  Elimination Rule:
  ```
  //
    Γ ⊢ A ∨ B
    Γ ⊢ A → C
    Γ ⊢ B → C
  -------------- (∨-elim)
      Γ ⊢ C
 ```

- Truth

  Formation Rule:
  ```
  //
  ----------------------
    ⊤ is a proposition
  ```

  Introduction Rule:
  ```
  //
  ---------- (⊤-intro)
    Γ ⊢ ⊤
  ```

- Falsity

  Formation Rule:
  ```
  //
  ----------------------
    ⊥ is a proposition
  ```

  Elimination Rule (The Principle of Explosion):
  ```
    Γ ⊢ ⊥
  --------- (⊥-elim)
    Γ ⊢ X
  ```

  Then we define that ¬P ≡ P → ⊥

-


## Examples

- Prove `{ (A ∧ B) ∧ C } ⊢ A ∧ ( B ∧ C )`:

  ```
  Let Γ = { ( A ∧ B ) ∧ C }

  -------------------- (hyp)                               ----------------(hyp)
    Γ ⊢ (A ∧ B) ∧ C              Γ ⊢ A ∧ B                Γ ⊢ (A ∧ B) ∧ C
  -------------------- (∧-elimL) ------------ (∧-elimR)   ----------- (∧-elimR)
    Γ ⊢ A ∧ B                       Γ ⊢ B                   Γ ⊢ C
  ------------- (∧-elimL)        ------------------------------------ (∧-intro)
      Γ ⊢ A                                   Γ ⊢ B ∧ C
  -------------------------------------------------------------------- (∧-intro)
                  Γ ⊢ A ∧ (B ∧ C)
  ```

- Prove `⊢ (A ∨ B) -> (B ∨ A)`

  ```
  //
                    ----------- (hyp)           ----------- (hyp)
                      Γ,A ⊢ A                     Γ,B ⊢ B
                  -------------- (∨-introR)   -------------- (∨-introL)
                    Γ,A ⊢ B ∨ A                Γ,B ⊢ B ∨ A
  --------- (hyp) ---------------- (→-intro) ----------------- (→-intro)
  Γ ⊢ A ∨ B       Γ ⊢ A → B ∨ A             Γ ⊢ B → B ∨ A
  ------------------------------------------------------------------- (∨-elim)
                          Γ={A ∨ B} ⊢ B ∨ A
                      ----------------------- (→-intro)
                        ⊢ (A ∨ B) → (B ∨ A)
  ```

- Prove ⊢ A → ¬¬A

  ```
  //
  ---------- (hyp) ------ (hyp)
  Γ ⊢ A → ⊥       Γ ⊢ A
  -------------------------- (→-elim)
    Γ = {A, (A → ⊥)} ⊢ ⊥
  --------------------- (→-intro)
    {A} ⊢ (A → ⊥) → ⊥
  -------------------------- (→-intro)
    ⊢ A → ((A → ⊥) → ⊥)
  ----------------------- (≡)
        ⊢ A → ¬¬A
  ```

## Exercise

- Prove ⊢ (A → B → C) → (A → B) → A → C

  ```
  //
  ---------------- (hyp)  ----- (hyp)  ----------- (hyp)  ------ (hyp)
  Γ ⊢ (A → B → C)        Γ ⊢ A          Γ ⊢ A → B         Γ ⊢ A
  -------------------------------- (→-elim) ----------------------- (→-elim)
              Γ ⊢ B → C                             Γ ⊢ B
 -------------------------------------------------------------- (→-elim)
                    Γ = {A → B → C, A → B, A} ⊢ C
                ---------------------------------- (→-intro)
                      {A → B → C, A → B} ⊢ A → C
                ----------------------------------- (→-intro)
                    {A → B → C} ⊢ (A → B) → A → C
            -----------------------------------------(→-intro)
                  ⊢ (A → B → C) → (A → B) → A → C
  ```

- Prove ⊢ (¬A ∨ ¬B) → ¬ (A ∧ B)

  ```
  //
  ```
