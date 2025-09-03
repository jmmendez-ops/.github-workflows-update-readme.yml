name: Update README

on:
  schedule:
      - cron: '0 0 * * *'  # Runs at 00:00 UTC everyday
        workflow_dispatch:  # Allows manual trigger
          push:
              branches: [ main ]

                jobs:
                  update-readme:
                      name: Update Profile README
                          runs-on: ubuntu-latest

                                  steps:
                                        - uses: actions/checkout@v2

                                                    # Updates Recent Activity
                                                          - uses: jamesgeorge007/github-activity-readme@master
                                                                  env:
                                                                            GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
                                                                                    with:
                                                                                              COMMIT_MSG: 'Update activity section'
                                                                                                        MAX_LINES: 5
                                                                                                        
                                                                                                              # Generate snake animation
                                                                                                                    - uses: Platane/snk@master
                                                                                                                            id: snake-gif
                                                                                                                                    with:
                                                                                                                                              github_user_name: jmmendez-ops
                                                                                                                                                        svg_out_path: dist/github-contribution-grid-snake.svg
                                                                                                                                                                  
                                                                                                                                                                        # Push changes
                                                                                                                                                                              - name: Push changes
                                                                                                                                                                                      uses: EndBug/add-and-commit@v7
                                                                                                                                                                                              with:
                                                                                                                                                                                                        branch: main
                                                                                                                                                                                                                  message: 'Update profile README'
