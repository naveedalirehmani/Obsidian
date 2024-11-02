https://vddvd33-my.sharepoint.com/:w:/g/personal/sss_vddvd33_onmicrosoft_com/Ef1lPH0rmHFPqqp0LH6u5pIBiob_EjY3EEGRPVjYmgC5wQ?rtime=f0Lw1tTF3Eg



Here’s a structured unit test report for the Solidity smart contract `Election`. Each test case is written based on the functional requirements. The tests will be for core functionalities, ensuring correctness and robustness.


### Functional Test Report for Election DApp (Frontend + Smart Contract)

| **Action**                                                   | **Expected Result**                                       |
|--------------------------------------------------------------|-----------------------------------------------------------|
| **Initialize Election on Page Load**                         | Election name and status (started/ended) displayed correctly. |
| **Display Candidates List**                                  | All candidates with name, party, symbol, and vote count are listed. |
| **Admin Adds Candidate from GUI**                            | Candidate added and displayed in the candidate list before the election starts. |
| **Admin Authorizes Voter from GUI**                          | Voter status is updated to authorized in the system and on the UI. |
| **Admin Starts Election from GUI**                           | Election status changes to ongoing, candidates can now receive votes. |
| **Voter Casts Vote via GUI**                                 | Voter can select a candidate and successfully submit the vote, vote count updates on UI. |
| **Admin Ends Election from GUI**                             | Election status changes to ended, no further votes allowed. |
| **Display Election Results**                                 | After election ends, results show candidate names and final vote counts. |
| **Unauthorized Voter Attempts to Vote**                      | Voter receives error message indicating they are not authorized. |
| **Voter Attempts to Vote Multiple Times**                    | UI blocks voter from voting more than once, error message displayed. |
| **Display Total Number of Votes Cast**                       | Total votes display correctly on the election results page. |

This report outlines the key actions that should be tested to ensure the frontend communicates correctly with the smart contract and handles user interactions as expected.