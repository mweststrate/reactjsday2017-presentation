# How types were introduced in MST (5 min)

Define another model (e.g. CreateUserPage) with compatible snapshot. (user & pwd & mail fields)
Union will throw because of multiple applicable types
Introduce a “type” field on each model, using types.literal to distinguish
