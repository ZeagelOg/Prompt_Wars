# Security Specification - VenueFlow

## Data Invariants
- Users are owners of their profiles.
- Roles are restricted: `attendee` is default. `staff` and `admin` must be granted.
- `crowd_snapshots` are write-only by staff and immutable.
- `predictions` are managed by system/staff and read-only for attendees.

## The Dirty Dozen Payloads
1. **Self-Escalation**: Attendee tries `setDoc` with `{ role: "admin" }`.
2. **Profile Theft**: User A tries to `setDoc` on `users/UserB`.
3. **Ghost Profile**: Creating a user profile without a matching `request.auth.uid`.
4. **Illegal Coordinates**: Snapshot with `latitude: 999`.
5. **Junk ID**: Creating user with ID `../../../etc/passwd`.
6. **Snapshot Tampering**: Updating an existing snapshot.
7. **Prediction Wipe**: Attendee calling `delete` on a gate prediction.
8. **Massive Payload**: `displayName` with 5MB of text.
9. **Role Swap**: Attendee trying to `update` their role to `staff`.
10. **Orphan Snapshot**: Snapshot without a valid `timestamp`.
11. **Anonymous Snoop**: Unauthenticated user trying to `list` predictions.
12. **Shadow Field**: Adding `isVerified: true` to a profile update.

## Test Matrix
| Payload | Collection | User Role | Expected |
|---------|------------|-----------|----------|
| 1       | users      | attendee  | DENY     |
| 2       | users      | attendee  | DENY     |
| 4       | snapshots  | attendee  | DENY     |
| 6       | snapshots  | staff     | DENY     |
| 7       | predictions| attendee  | DENY     |
| 9       | users      | attendee  | DENY     |
