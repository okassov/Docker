package kudo

import (
  "strconv"
  "github.com/{{ YOUR_GITHUB_USERNAME }}/kudo-oos/pkg/core"
)

type GitHubRepo struct {
  RepoID      int64  `json:"id"`
  RepoURL     string `json:"html_url"`
  RepoName    string `json:"full_name"`
  Language    string `json:"language"`
  Description string `json:"description"`
  Notes       string `json:"notes"`
}

type Service struct {
  userId string
  repo   core.Repository
}

func (s Service) GetKudos() ([]*core.Kudo, error) {
  return s.repo.FindAll(map[string]interface{}{"userId": s.userId})
}

func (s Service) CreateKudoFor(githubRepo GitHubRepo) (*core.Kudo, error) {
  kudo := s.githubRepoToKudo(githubRepo)
  err := s.repo.Create(kudo)
  if err != nil {
    return nil, err
  }
  return kudo, nil
}

func (s Service) UpdateKudoWith(githubRepo GitHubRepo) (*core.Kudo, error) {
  kudo := s.githubRepoToKudo(githubRepo)
  err := s.repo.Create(kudo)
  if err != nil {
    return nil, err
  }
  return kudo, nil
}

func (s Service) RemoveKudo(githubRepo GitHubRepo) (*core.Kudo, error) {
  kudo := s.githubRepoToKudo(githubRepo)
  err := s.repo.Delete(kudo)
  if err != nil {
    return nil, err
  }
  return kudo, nil
}

func (s Service) githubRepoToKudo(githubRepo GitHubRepo) *core.Kudo {
  return &core.Kudo{
    UserID:      s.userId,
    RepoID:      strconv.Itoa(int(githubRepo.RepoID)),
    RepoName:    githubRepo.RepoName,
    RepoURL:     githubRepo.RepoURL,
    Language:    githubRepo.Language,
    Description: githubRepo.Description,
    Notes:       githubRepo.Notes,
  }
}

func NewService(repo core.Repository, userId string) Service {
  return Service{
    repo:   repo,
    userId: userId,
  }
}

под конец не забудьте закомментировать дефолтные NTP сервера в /etc/chrony.conf

Эти снизу

server 0.centos.pool.ntp.org iburst
server 1.centos.pool.ntp.org iburst
server 2.centos.pool.ntp.org iburst
server 3.centos.pool.ntp.org iburst 

Если этого не сделать он будет стучаться в инет для синхронизации времени



 