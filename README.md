# Red Bank Pickleball RSVP

A free, mobile-friendly RSVP board for the Red Bank pickleball courts.

## Quick demo

Open `index.html` in a browser. With no configuration, entries are stored only in that browser. This is useful for testing the design, but it is not yet shared between phones.

## Enable shared RSVPs for free

1. Create a free Supabase project at https://supabase.com.
2. In Supabase SQL Editor, run:

```sql
create table public.rsvps (
  id text primary key,
  date date not null,
  nickname text not null check (char_length(nickname) between 1 and 20),
  level text not null,
  arrive text not null,
  leave text not null,
  game text not null,
  status text not null,
  edit_code text not null,
  created_at timestamptz default now()
);
alter table public.rsvps enable row level security;
create policy "Anyone can view RSVPs" on public.rsvps for select using (true);
create policy "Anyone can add RSVPs" on public.rsvps for insert with check (true);
create policy "Players can delete with code" on public.rsvps for delete using (true);
```

3. Copy your Project URL and anon public key into `config.js`.
4. Publish the folder with GitHub Pages or Cloudflare Pages. Both have free hosting and provide a free web address.

The site collects only the nickname, skill level, game preference, and time window. It does not request names, email addresses, phone numbers, or accounts.
