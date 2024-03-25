
### Seeding your database

It refers to adding some initial data into your database. This is useful as using `prisma migrate` sometimes deletes all your data in your database.

Create a `seed.ts` file.

Then add a command in your `package.json`.

```json
"prisma": {
	"seed": "ts-node --transpile-only prisma/seed.ts"
}
```

We added `transpile-only` flag as it skips type checking and saves us some execution time.

Now, every time you run `prisma db seed` or use `prisma migrate dev` or `prisma migrate reset`, it will run the `seed.ts` file.

To skip seeding, use the `skip-seed` flag, e.g. `prisma migrate --skip-seed`.

